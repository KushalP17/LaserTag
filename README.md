# LaserTag

A Bop It! style laser tag game.

## Overview

TODO

## Development

Guide to getting started with working on this project.

### Prerequisites

1. Install ESP-IDF (Espressif IoT Development Framework) for building firmware targeting the ESP32.

   See [https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/).

   Alternatively, see the [Docker](#docker) section.

   For information on how ESP-IDF is used in this project, see the [ESP-IDF](#esp-idf) section.

### Procedure

1. Clone the repository.

   Make sure to include the `--recurse-submodules` option when cloning, e.g. `git clone git@github.com:delta-12/LaserTag.git --recurse-submodules`.

2. Open an issue or contribute to an exisitng issue.

   A branch associated with the issue must be created for any changes needed to resolve the issue.

3. Make changes to the project.

   All changes must be made on the branch associated with the issue they are a part of. Changes must not be made on `main` or `develop`. These branches are to be updated only through pull requests. All commit messages must contain the name of the branch containing the commit and a description of the changes included in the commit.

4. Open a pull request.

   Code submitted in a pull request must have been thoroughly tested and verified to work. All pull requests must be linked to an issue. The base ref may be the `develop` branch, which contains the latest changes verified to work. `main`, on the other hand, is only for releases of production code and artifacts. Do not request to merge changes directly into `main`.

5. Close the issue if resolved.

   Close the issue if the changes in the pull request resolved the issue and the pull request was approved and merged. Any branches associated with the issue should be deleted when issue is resolved.

### ESP-IDF

Firmware for this project targets the ESP32, and as such, ESP-IDF is used for firmware development.

#### Build

    Firmware for a device can be built by navigating to the directory within the repository that contains the firmware targetting the particular device and running the build command.

    `idf.py build`

#### Flash and Monitor

    Firmware can be flashed a device with ESP-IDF using the flash command.

    `idf.py -p PORT flash`

    Replace `PORT` with the port of the device you are flashing, e.g. `idf.py -p /dev/ttyUSB0 flash`.

    After flashing a device, its output can be monitored using the monitor command.

    `idf.py -p PORT monitor`

    Again, replace `PORT` with the port of the device you are monitoring, e.g. `idf.py -p /dev/ttyUSB0 monitor`.

    These two commands can also be combined as follows:

    `idf.py -p PORT flash monitor`

    e.g. `idf.py -p /dev/ttyUSB0 flash monitor`

#### Configuration menu

    ESP-IDF provides a graphical menu for configuring project settings such as config defines and build settings.  The configuration menu can be accessed by running the following command.

    `idf.py menuconfig`

### Docker

If you do not wish to install ESP-IDF, the ESP-IDF Docker Image can be used instead. This may also be suitable for environments in which it is diffcult to install or use ESP-IDF. Obviously, Docker is required for this approach. For instructions to setup Docker, see [https://www.docker.com/get-started/](https://www.docker.com/get-started/).

1. Navigate to the project directory and build the firmware with the docker command

   `docker run --rm -v $PWD:/project -w /project -u $UID -e HOME=/tmp espressif/idf idf.py build`

2. To flash the firmware, run

   `docker run --rm -v $PWD:/project -w /project -u $UID -e HOME=/tmp --device=/dev/ttyUSB0 espressif/idf idf.py -p /dev/ttyUSB0 flash`

   To monitor after flashing, run

   `docker run --rm -v $PWD:/project -w /project -u $UID -e HOME=/tmp --device=/dev/ttyUSB0 -it espressif/idf idf.py -p /dev/ttyUSB0 monitor`

   The flash and monitor commands can be combined into a single command as follows

   `docker run --rm -v $PWD:/project -w /project -u $UID -e HOME=/tmp --device=/dev/ttyUSB0 -it espressif/idf idf.py -p /dev/ttyUSB0 flash monitor`

The firmware can also be configured by running

`docker run --rm -v $PWD:/project -w /project -u $UID -e HOME=/tmp -it espressif/idf idf.py menuconfig`

Note: These commands assume the environment is a Debian-based Linux distribution with the target device connected on port `/dev/ttyUSB0`.
