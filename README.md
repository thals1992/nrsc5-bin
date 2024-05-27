# nrsc5

This program receives NRSC-5 digital radio stations using an RTL-SDR dongle. It offers a command-line interface as well as an API upon which other applications can be built. Before using it, you'll first need to compile the program using the build instructions below.

You can test the program using the included sample capture:

    $ xz -d < ../support/sample.xz | src/nrsc5 -r - 0

## Usage

### Command-line options:

    frequency                       center frequency in MHz or Hz
                                      (do not provide frequency when reading from file)
    program                         audio program to decode
                                      (0, 1, 2, or 3)
    -g gain                         gain
                                      (example: 49.6)
                                      (automatic gain selection if not specified)
    -d device-index                 rtl-sdr device
    -p ppm-error                    rtl-sdr ppm error
    -H rtltcp-host                  rtl_tcp host with optional port
                                      (example: localhost:1234)
    -r iq-input                     read IQ samples from input file
    -w iq-output                    write IQ samples to output file
    -o audio-output                 write audio to output file
    -t audio-type                   type of audio output (wav or raw)
                                      (default is wav. used in conjunction with -o)
    -q                              disable log output
    -l log-level                    set log level
                                      (1 = DEBUG, 2 = INFO, 3 = WARN)
    -v                              print the version number and exit
    --am                            receive AM signals
                                      (default is FM)
    -T                              enable bias-T
    -D direct-sampling-mode         enable direct sampling
                                      (1 = I-ADC input, 2 = Q-ADC input)
    --dump-aas-files dir-name       dump AAS files
                                      (WARNING: insecure)
    --dump-hdc file-name            dump HDC packets

### Examples:

Tune to 107.1 MHz and play audio program 0:

    $ nrsc5 107.1 0

Tune to 107.1 MHz and play audio program 0. Manually set gain to 49.0 dB and save raw IQ samples to a file:

    $ nrsc5 -g 49.0 -w samples1071 107.1 0

Read raw IQ samples from a file and play back audio program 0:

    $ nrsc5 -r samples1071 0

Tune to 90.5 MHz and convert audio program 0 to WAV format for playback in an external media player:

    $ nrsc5 -o - 90.5 0 | mplayer -

### Keyboard commands:

To switch between audio programs at runtime, press <kbd>0</kbd> through <kbd>7</kbd>.

To quit, press <kbd>Q</kbd>.

### RTL-SDR drivers on Windows

If you get errors trying to access your RTL-SDR device, then you may need to use [Zadig](http://zadig.akeo.ie/) to change the USB driver. Once you download and run Zadig, select your RTL-SDR device, ensure the driver is set to WinUSB, and then click "Replace Driver". If your device is not listed, enable "Options" -> "List All Devices".
