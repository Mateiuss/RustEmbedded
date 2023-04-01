# Workshop course

Through this `README` you should be able to flash the tock kernel on a board.

# Gettings Started

In order to be able to use tock and flash it on the board using Windows, you will need to import the following VM:<br>
[Virtual Machine for TockOS](https://drive.google.com/file/d/1nOcma5LbAHTYcOc32b-BdwE1kQZfWcyG/view?usp=share_link)

If you are a **Linux** user you also can use the VM, which is strongly recommended.

If you are a **MacOS** user you need to follow the staps bellow.

# Requirements

In order to use tock we need to install some tools:

1. First make sure you updated the packages:
    ```bash
    sudo apt update && sudo apt upgrade # For Linux
    brew update                         # For Mac
    ```

2. Clone the Tock `kernel` repository and `libtock-c`:
    ```bash
    git clone https://github.com/Matrix22/tock.git
    git clone https://github.com/tock/libtock-c.git
    ```

3. Install `Rust`:
    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

    # And follow the installation process
    ```
4. Install `arm-none-eabi toolchain`. This enables you to compile apps written in C for Cortex-M boards:
    ```bash
    # MacOS
    brew tap ARMmbed/homebrew-formulae && brew update && brew install arm-none-eabi-gcc

    # Linux
    sudo apt install gcc-arm-none-eabi
    ```

5. Install `openOCD` in order to flash the board:
    ```bash
    # MacOS
    brew install open-ocd

    # Linux
    sudo apt install openocd
    ```

6. Install `tockloader`. This is an all-in-one tool for programming boards and using Tock and also for accessing the console:
    ```bash
    pip3 install -U --user tockloader

    # MacOS
    export PATH=$HOME/Library/Python/3.9/bin/:$PATH

    # Linux
    PATH=$HOME/.local/bin:$PATH
    ```

    You will need to `export` the `PATH` every time you close your terminal session.

Congratulations you installed the TockOS and it's dependencies, know let's test if it works.

# Compiling the kernel

Now that we are all set up let's compile and upload the kernel binary to our board.

For this course we will use a `Microbit v2`.

1. Navigate to the `tock` repository and change the branch to `better-process-console`:
    ```bash
    cd tock
    git checkout better-process-console

    # Check that you successfully changed the branch
    git branch -a

    # You should see same output:
    # * better-process-console
    # master
    # ...
    ```

2. Plug the `Microbit: v2` into your computer and make sure that your system recognizes the board.

2. Navigate to the `microbit_v2` utilities in the repository:
    ```bash
    cd boards/microbit_v2
    make flash
    ```

3. Open another terminal and try to access the boards `console`:
    ```bash
    tockloader listen

    # This should open you a prompt in tockOS
    tock$
    ```

    If you do not see the prompt press the `RESET` button on the `Microbit: v2` board.<br>
    If you want to close the console session press `Ctrl + C` interrupt signal.

This is your first interaction with the tockOS be proud of yourselves.

# Run an app on board

Make sure you have installed the `libtock-c` repository

1. Navigate to the blink application:
    ```bash
    cd libtock-c/examples/blink

    # Compile the blink application
    make

    # Install the application
    tockloader install
    ```

    If you are not able to install the blink app you can install it via `app store`:
    ```bash
    tockloader install blink
    ```

2. Now turn the microbit around and observe the magic ... isn't it beautiful?

3. You can install any of available apps from the `examples` folder, you can even play music on it or you can right your own `drivers` in order to do different things.<br>
    Playaround a bit and get used to flashing the board

4. In order to delete an app or all apps you can run:
    ```bash
    tockloader uninstall blink

    # For all apps
    tockloader erase-apps
    ```

For more details access the [Tock Book](https://book.tockos.org/introduction.html)
