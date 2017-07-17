### Blinky on mbed CLI

Blinky is a very simple program that blinks the LED on your board every half second. We use Blinky to show you how to import, build and flash an application.

#### Quick start video

<span class="images">[![Video tutorial](http://img.youtube.com/vi/PI1Kq9RSN_Y/0.jpg)](https://www.youtube.com/watch?v=PI1Kq9RSN_Y)<span>Watch how to create your first application on mbed CLI</span></span>

<span class="notes">**Note:** the video assumes you've already [installed mbed CLI](#installing-mbed-cli-and-a-toolchain).

#### Blinky's code

>>> C
>>>

Blinky's code is a simple `while` loop inside the `main()` function:

>>> C
```
#include "mbed.h"
#include "rtos.h"

DigitalOut led1(LED1);

// main() runs in its own thread in the OS
// (note the calls to wait below for delays)
int main() {
    while (true) {
        led1 = !led1;
        wait(0.5);
    }
}
```
>>>

#### Installing mbed CLI and a toolchain

mbed CLI is an offline tool, meaning you'll have to install it before you can work. You will also need to install a toolchain. Please follow the installation instructions on the [mbed CLI page](../dev_tools/cli.md), and come back here when you're done.

#### Setting context

>>> C
>>>

Whenever you work with mbed CLI, you need to navigate your command-line terminal to the directory in which you want to work. For example, if your program is in a folder called ``my_program``:

>>> C
```
cd my_program
```
>>>

You can then start running mbed CLI commands, and they will run in the correct context.

#### Getting Blinky

mbed CLI can import Blinky, along with the mbed OS codebase. The import process creates a new directory as a subdirectory of your current context (as explained above).

To import Blinky, from the command-line:

>>> C
>>>

1. Navigate to a directory of your choice. We're navigating to our development directory:

  >>> C
  ```
  cd dev_directory
  ```
  >>>

2. Import the example:

  >>> C
  ```
  mbed import mbed-os-example-blinky
  cd mbed-os-example-blinky
  ```
  >>>

<span class="tips">**Tip:** ``import`` requires a full URL to Mercurial or GitHub. If you don't enter a full URL, mbed CLI prefixes your snippet with ``https://github.com/ARMmbed/``. We took advantage of this feature in our example; ``import mbed-os-example-blinky`` is interpreted as ``https://github.com/ARMmbed/mbed-os-example-blinky``.</span>

Blinky is now under `dev_directory` > `mbed-os-example-blinky`. You can look at `main.cpp` to familiarize yourself with the code.

#### Compiling

Invoke `mbed compile`, specifying:

* Your board: ``-m <board_name>``.
* Your toolchain: ``-t <GCC_ARM`, `ARM` or `IAR`>``.

>>> C
>>>

For example, for the board K64F and the ARM Compiler 5:

>>> C
```
mbed compile -m K64F -t ARM
```
>>>

Your PC may take a few minutes to compile your code. At the end you should get the following result:

>>> C
```
[snip]
+----------------------------+-------+-------+------+
| Module                     | .text | .data | .bss |
+----------------------------+-------+-------+------+
| Misc                       | 13939 |    24 | 1372 |
| core/hal                   | 16993 |    96 |  296 |
| core/rtos                  |  7384 |    92 | 4204 |
| features/FEATURE_IPV4      |    80 |     0 |  176 |
| frameworks/greentea-client |  1830 |    60 |   44 |
| frameworks/utest           |  2392 |   512 |  292 |
| Subtotals                  | 42618 |   784 | 6384 |
+----------------------------+-------+-------+------+
Allocated Heap: unknown
Allocated Stack: unknown
Total Static RAM memory (data + bss): 7168 bytes
Total RAM memory (data + bss + heap + stack): 7168 bytes
Total Flash memory (text + data + misc): 43402 bytes
Image: .\.build\K64F\ARM\mbed-os-example-blinky.bin             
```
>>>

The program file, ``mbed-os-example-blinky.bin``, is under your ``mbed-os-example-blinky\build\K64F\ARM\`` folder.

#### Programming your board

>>> C
>>>

mbed Enabled boards are programmable by drag and drop over a USB connection.

>>> C
```
1. Connect your mbed board to the computer over USB.
2. Copy the binary file to the board. In the example above, the file is ``mbed-os-example-blinky.bin``, and it's under the ``mbed-os-example-blinky\build\K64F\ARM\`` folder.
3. Press the reset button to start the program.
```
>>>

You should see the LED of your board turning on and off.