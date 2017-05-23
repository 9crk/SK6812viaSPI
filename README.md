# SK6812viaSPI
This repo contains basic driver code in C++ & Arduino C++ that allows you to drive SK6812, WS2812, WS2812B/Neopixels using the SPI port. Only the MOSI(DATA) pin of the SPI port is required. Below are the platforms that this has been tested on.
HIGHLY recomend using pixel 0 as a NULL pixel to boost 3.3v to 5v for all 3.3v boards or an equivelent high speed Voltage Level Shifter.

# ESP8622
YES

# Raspberry Pi via BCM2835 libarry 
YES but NO. SPI Transfers "can and will" be interupted by the OS, as your program runs in userspace so this will probbaly never work

# Raspberry Pi via SPIDEV
YES - Make sure your spi bufsiz=LARGE_ENOUGH NumofPixels x 12 = bytes per SPIFrame required

# NanoPi Neo Air (using the Matrix GPI library)
YES

# NanoPi Neo Air (using native SPIDEV)

YES - Make sure your spi bufsiz=LARGE_ENOUGH NumofPixels x 12 = bytes per SPIFrame required
* Create an executable script in /root
		
    > nano /root/setSPIBufSize
    
*	Add the following 2 lines, note im setting the buffer size to 1024000 bytes

		> chmod 666 /sys/module/spidev/parameters/bufsiz
		> echo 1024000 > /sys/module/spidev/parameters/bufsiz
* Make the file executable 
    
    > chmod 777 /root/setSPIBufSize
    
* Edit the startup script /etc/rc/local and add the following line

    > sudo nano /etc/rc/local
  	> sudo /root/setSPIBufSize

* Reboot the device and check that the setting has been done

  >cat /sys/module/spidev/parameters/bufsiz
  This should output 1024000
  
  
# STM32F103C(bluepill)
YES  
