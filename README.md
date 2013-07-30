Media Library Generator
===

This script is used to generate media libraries. Currently it supports random generation of audio (Mp3) and image (jpg, png, gif and tiff) files. The script generates a random directory structure, in which it then places media files generated with random input. The media files are encoded using common encoding softwares, such as LAME and ImageMagick (dependencies are listed below). The actual multimedia contents of the generated files are random, which means the audio files are not very pleasurable to listen to, and the image files are rather abstract - the contents are however correct to the specification of the multimedia formats.

The media files contain roughly sensible metadata, which is currently not fuzzed, even though this is a planned feature. This means metadata fields intended to contain names of people are set to.. common names of people. Fields for longer text strings (such as descriptions, copyrights and licenses) contain short generated english sentences. Fuzzy input, such as uncommon or invalid characters can be added to the corpus contained in Sentences.py if desired.

### Why would you want this script?
* Metadata can be generated with a relatively high quality. By generating media files, rather than gathering them from other sources, time and bandwidth can be saved
* The randomness used in the script is generated by the default deterministic PRNG (the Mersenne twister) of Python 2 (I use 2.7.3), which can be seeded. This means that every aspect of the generated media library is correctly replicated if the script is re-run with the same parameters at a later time or place
* The metadata fields to be included can be randomized using the `--brokenness` parameter of the respecive generators
* Very, very large media libraries can be generated with ease

### Usage
Run the script without any parameters to see the available parameters. The generator parameter is mandatory, the rest are optional. When a parameter has not been set, a random value is chosen.

The generator modules sometimes have module-specific configuration options, you can list these by issuing `--help` after selecting a generator module: `python MLG.py MP3FileGenerator --help`.

### Dependencies
In order to generate MP3 files, an installation of LAME (http://lame.sourceforge.net/) is required. LAME 3.99.5 is known to work, later (and probably earlier) versions should also work.

The `id3v2` tool (http://id3v2.sourceforge.net/) is used to tag the MP3 files generated by LAME, since LAME is not able to set all the desired tags, you will need this also.

In order to generate album art for the MP3 files, ImageMagick (http://www.imagemagick.org), and specifically the `convert` tool is required. This tool is also used to generate the image files in the image generator.

The generated image files are tagged using `exiftool` (http://www.sno.phy.queensu.ca/~phil/exiftool/).

### Caveats
Reproducibility is a major feature of this script. Changes to the script which involve adding or subtracting usage of the PRNG will affect the generated media library. This means future versions of the script will not produce the same libraries as older versions. If you intend on reproducing a library, please ensure the exact same version of the script is used at all times.

Different versions of Python may contain different PRNGs. The same PRNG needs to be used if the results of the script are to be reproduced. The script is also dependent on the fact that the PRNG is deterministic and seedable.

Different versions of the encoding software used may produce different outputs for the same input. If you wish to reproduce the exact same multimedia contents of your files, you should ensure that the versions of the encoding software coincides.

### Contact
Send any questions to jonatan.palsson at pelagicore dot com. Pull requests on GitHub are of course welcome.
