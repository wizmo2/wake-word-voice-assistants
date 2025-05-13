---
title: "ESP32-S3-Touch voice assistant"
product_name: ESP32-S3-TOUCH
device_name_entry: ESP32-S3-TOUCH
config_link: /voice_control/s3_box_voice_assistant/#to-delete-the-configuration-from-esphome
related:
  - docs: /voice_control/troubleshooting/
    title: General troubleshooting section for Assist
  - docs: /voice_control/troubleshooting_the_s3_touch/
    title: Troubleshooting the ESP32-S3-TOUCH
  - docs: /common-tasks/os/#configuring-access-to-files
    title: Access to your configuration files
  - docs: /voice_control/about_wake_word/
    title: Enable wake word
  - docs: /voice_control/s3-touch-customize/#customizing-on-device-wake-words-microwakeword
    title: Customizing the S3-TOUCH with on-device wake words
  - url: https://esphome.io/projects/index.html
    title: ESPHome projects page
---

This tutorial will guide you to turn an ESP32-S3-TOUCK-1.85IN into a Home Assistant voice assistant. Note, the term ESP32-S3-TOUCH may be used to refer to any of the 3 product variants.

<lite-youtube videoid="erf7HqTwCGs" videotitle="Okay Nabu! Open-source voice assistant running on an WaveShare ESP32-S3-Touch
"></lite-youtube>

## Prerequisites

- Home Assistant 2025.2 or later, installed with the Home Assistant Operating System. If you do not have Home Assistant installed yet, refer to the [installation page](/installation/) for instructions.
- [Home Assistant Cloud](/voice_control/voice_remote_cloud_assistant/) or a manually configured [Assist Pipeline](/voice_control/voice_remote_local_assistant)
- The password to your 2.4&nbsp;GHz Wi-Fi network
- Chrome or Edge browser on a desktop (not Android/iOS)
- One of the WaveShare ESP32-S3-Touch-LCD-1.85C-BOX with Speaker:
- USB-C cable to connect the ESP32-S3-TOUCH
- This procedure assumes that this is the first time you are installing ESPHome firmware on the device. If you have previously completed this tutorial and now want to install the latest software version, follow the steps on [updating the software on the S3-TOUCH](#updating-the-software-on-the-s3-touch).

## Installing the software onto the ESP32-S3-TOUCH

Before you can use this device with Home Assistant, you need to install a bit of software on it.

{% tabbed_block %}

- title: Using the ESP32-S3-TOUCH
  content: |

    1. These steps apply to the ESP32-S3-TOUCH. Make sure this page is opened in a Chromium-based browser on a **desktop**. The software installation does not work with a tablet or phone.

       - Select the **Connect** button below to display a list of available USB devices. Do not connect the ESP32-S3-TOUCH yet. We want to see the list of available USB devices first, so that it is easier to recognize the ESP device afterward.
       - If your browser does not support web serial, you will see a warning message indicating this instead of a button.

           <script type="module" src="https://unpkg.com/esp-web-tools@10/dist/web/install-button.js?module"></script>
           <esp-web-install-button manifest="https://firmware.esphome.io/wake-word-voice-assistant/esp32-s3-touch/manifest.json"></esp-web-install-button>

       - **For advanced users**: The configuration files are available on GitHub:
         - [ESP32-S3-TOUCH config on GitHub](https://github.com/wizmo2/wake-word-voice-assistants/blob/add-waveshare-touch/esp32-s3-touch-1.85/esp32-s3-touch-1.85.yaml)

    2. To connect the ESP32-S3-TOUCH to your computer, follow these steps:
       - In the pop-up window, view the available ports.
       - Plug the USB-C cable into the box directly, not into the docking station (not into the blue part) and connect it to your computer.
       - **Troubleshooting**: If your ESP32-S3-TOUCH does not appear in the list of devices presented by your browser, you need to manually invoke "flash mode":
         - Hold the "boot" button (left side upper button) as you tap the "reset" button (left side lower button).
         - After a few seconds, the ESP32-S3-TOUCH should appear in the list of USB devices presented by your browser.
         - Follow the steps until step 3. After selecting the **Next** button, on the S3-Box, tap the "Reset" button again.
         - Then, select the blue **Connect button** again, select the USB device and follow the prompts to configure the Wi-Fi.
         - In the pop-up window, there should now appear a new entry. Select this USB serial port and select **Connect**.
    3. Select **Install Voice Assistant**, then **Install**.
         - Once the installation is complete, select **Next**.
         - Add the ESP32-S3-TOUCH to your Wi-Fi:
           - When prompted, select your network from the list and enter the credentials to your 2.4&nbsp;GHz Wi-Fi network.
           - Select **Connect**.
           - The ESP32-S3-TOUCH now joined your network. Select **Add to Home Assistant**.
    4. This opens the **My** link to Home Assistant.
       - If you have not used My Home Assistant before, you will need to configure it. If your Home Assistant URL is not accessible on `http://homeassistant.local:8123`, replace it with the URL to your Home Assistant instance.
       - Open the link.
       ![Open My link](/images/assist/esp32-atom-flash-06.png)
    5. Select **OK**.

       ![Set up ESPHome](/images/assist/esp32-atom-flash-07.png)
    6. To add the newly discovered device, select the ESP32-S3-TOUCH from the list.
       - Add your ESP32-S3-TOUCH to a room and select **Finish**.
    7. You should now see the **ESPHome** integration.
       ![New ESPHome device discovered](/images/assist/m5stack-atom-echo-discovered3.png)

    8. Select the **ESPHome** integration. Under **Devices**, you should see the **ESP32-S3-TOUCH** listed.
        ![ESP32-S3-TOUCH discovered](/images/assist/s32-s3-touch-discovered.png)

        - Your ESP32-S3-TOUCH is connected to Home Assistant over Wi-Fi. You can now move it to any place in your home with a USB power supply.

{% endtabbed_block %}

## Checking wake word settings

1. Make sure your assistant has [wake word enabled](/voice_control/install_wake_word_add_on/), using "OK Nabu".
2. Under **Devices**, on the ESP32-S3-TOUCH* entry, select **Device** to open the device page.
3. Check the device settings:
    - If you want, you can process the wake word on the ESP32-S3 device, rather than on your Home Assistant server.   (The server is the device where Home Assistant is installed, for example on Home Assistant Green):
    - Under **Wake word engine location**, select **On device**, if you want your wake word to be processed on the device itself, and not in Home Assistant.
      - Local processing is faster.
      - The wake word is now *Okay Nabu*.

      ![ESP32-S3-TOUCH on device wake word processing](/images/assist/wake_word_engine_location.png)

4. If you chose on-device wake word, but you do not want to use *Okay Nabu*, you can change the on-device wake word.
   - Currently, *Hey Jarvis* or *Alexa* are the supported alternatives.
   - To change your wake word, follow the steps in [Customizing the S3-TOUCH with on-device wake words](/voice_control/s3-touch-customize/#customizing-on-device-wake-words-microwakeword).
5. Congratulations! You can now voice control Home Assistant via a ESP32 device with a display. Now give some commands.

## Controlling Home Assistant

1. Say your wake word. For this tutorial, use "OK Nabu", or tap the top-right `IO0` button, or tap the "Cassita" icon on the screen. 
2. Say a [supported voice command](/voice_control/builtin_sentences/). For example, *Turn on the light*.
   - Once the intent has been processed, the LED lights up in green and Home Assistant confirms the action.
      - Make sure you’re using the area name exactly as you defined it in Home Assistant.
      - You can also ask a question, such as
          - *Is the front door locked?*
          - *Which lights are on in the living room?*
3. Your command is not supported? Add your own commands using [a sentence trigger](/voice_control/custom_sentences/).

## Turning off microphone or screen

1. If you do not want to Assist to listen to you for a while, you can turn off the microphone.
   - Double-click the top-right `IO01 button, or go to {% my integrations title="**Settings** > **Devices & Services**" %} and select the **ESPHome** integration.
      - Under **ESP32-S3-TOUCH**, select **1 device**.
      - Enable **Mute**.
      - The screen of the ESP32-S3-TOUCH will turn off, too.

      ![Toggle to enable/disable Mute](/images/assist/wake_word_disable.png)

2. If you want to just use the wake word, but do not want to use the screen, you can enable the auto screen timeout.
   - Go to {% my integrations title="**Settings** > **Devices & Services**" %} and select the **ESPHome** integration.
     - Under **ESP32-S3-TOUCH**, select **1 device**.
     - If you have not Enabled the function, Press "**Show All**" and enable "**Screen Off**" in the settings
     - Set a "**Screen Off**" time higher than 0 seconds.

      ![Toggle to enable/disable wake word](/images/assist/s3-touch-disable-screen.png)
## Extending the battery life

1. To put the unit into sleep mode
   - Press the top-right `IO0` button for 2 seconds and release 

2. If you want to extend the battery life, you can enable the auto sleep timeout.
   - Go to {% my integrations title="**Settings** > **Devices & Services**" %} and select the **ESPHome** integration.
     - Under **ESP32-S3-TOUCH**, select **1 device**.
     - If you have not Enabled the function, Press "**Show All**" and enable "**Auto Sleep**" in the settings
     - Set a "**Auto Sleep**" time higher than 0 seconds.

      ![Toggle to enable/disable wake word](/images/assist/s3-touch-enable-sleep.png)

3. To exit sleep mode, simply tap the screen.

## Factory reset

1. To reset the device, press the bottom-right `RST` button
1. To perform a factory reset, press and hold the top-right `IO0` button for 10 seconds.

## Updating the software on the S3-TOUCH

To update the software on your S3-TOUCH, follow the steps below that reflect your setup.

- **Option 1**: You have Home Assistant 2024.7 or later, and have not manually altered your ESPHome configuration for the S3-TOUCH:
  - Once an update is available, you will receive an update notification, just like any other update.
  - To install the precompiled new firmware directly on your box, make sure the S3-TOUCH is connected to your network, and under **ESP32 S3 TOUCH...Firmware**, select **Install**.
- **Option 2**: You have Home Assistant 2024.6 or older, and have not manually altered your ESPHome configuration for the S3-TOUCH:
  - Follow steps 1 of the procedure on [installing the software onto the S3-TOUCH](#installing-the-software-onto-the-esp32-s3-touch).
    - This installs the latest, precompiled firmware for your S3-TOUCH.
- **Option 3**: You have manually changed the configuration file for your S3-TOUCH:
  - You need to compile your own firmware. To do so, either:
    - Use the ESPHome dashboard add-on within Home Assistant. While the easiest option, it tends to be the slowest and may fail, particularly on older systems or on systems with limited memory/CPU resources.
    - Follow the steps in the [ESPHome documentation](https://esphome.io/guides/getting_started_command_line) and use a desktop-class system to compile and install the firmware. Initial setup is more complex, but the process is significantly faster and more reliable.