from django.db import models
from django.utils.translation import gettext_lazy as _
from django.db.models.signals import post_save
from django.dispatch import receiver


class Artist(models.Model):
    n_artist = models.CharField(_("Artist"), max_length=150)

    class Instruments(models.TextChoices):
        GUITAR = "Guitar", _("Guitar")
        BASS = "Bass", _("Bass")
        DRUMS = "Drum", _("Drums")
        VOCAL = "Vocal", _("Vocal")
        PIANO = "Piano", _("Piano")
        OTHER = "Other", _("Other")
    i_artist = models.CharField(
        _("Instrument"), max_length=10, choices=Instruments.choices)
    date_started = models.DateField(
        _("Date of Integration"), auto_now=False, auto_now_add=False)
    active = models.BooleanField(_("Is Active?"), default=True)

    class Meta:
        db_table = ''
        managed = True
        verbose_name = 'Artist'
        verbose_name_plural = 'Artists'

    def __str__(self) -> str:
        return self.n_artist


class Band(models.Model):
    n_band = models.CharField(_("Name of the Band"), max_length=150)
    members = models.ManyToManyField(Artist, _("Members_Band"))
    date_band = models.DateField(
        _("Date of formation"), auto_now=False, auto_now_add=False)
    logo = models.ImageField(
        _("Band's Logo"), upload_to="band/", default="band/default.webp", height_field=None, width_field=None, max_length=None)
    numbers_disk = models.IntegerField(_("Number of Disks"), default=0)

    class Meta:
        db_table = ''
        managed = True
        verbose_name = 'Band'
        verbose_name_plural = 'Bands'

    def __str__(self):
        return self.n_band


class Disk(models.Model):
    n_disk = models.CharField(_("Name of the Disk"), max_length=150)
    author = models.ForeignKey(
        Band, verbose_name=_("Autor"), on_delete=models.SET_NULL, null=True)
    date_debut = models.DateTimeField(
        _("Date of debut"), auto_now=False, auto_now_add=False)

    class Meta:
        db_table = ''
        managed = True
        verbose_name = 'Disk'
        verbose_name_plural = 'Disks'

    def __str__(self) -> str:
        return self.n_disk


@receiver(post_save, sender=Disk)
def update_band_numbers_disk(sender, instance, created, **kwargs):
    if created:
        instance.author.numbers_disk += 1
        instance.author.save()
