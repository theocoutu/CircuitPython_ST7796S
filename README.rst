Introduction
============



.. image:: https://img.shields.io/discord/327254708534116352.svg
    :target: https://adafru.it/discord
    :alt: Discord

.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code Style: Black

displayio driver for ST7796S TFT LCD displays


Dependencies
=============
This driver depends on:

* `Adafruit CircuitPython <https://github.com/adafruit/circuitpython>`_

Please ensure all dependencies are available on the CircuitPython filesystem.
This is easily achieved by downloading
`the Adafruit library and driver bundle <https://circuitpython.org/libraries>`_
or individual libraries can be installed using
`circup <https://github.com/adafruit/circup>`_.

Usage Example (CPv8)
====================

.. code-block:: python

    	import board
	import displayio
	import terminalio
	from adafruit_display_text import label
	from circuitpython_st7796s import ST7796S
	
	disp_spi = board.SPI() # OR # import busio;spi = busio.SPI(clock=board.PIN, MISO=board.PIN, MOSI=board.PIN)

	while not disp_spi.try_lock():  #
		pass		   	# Are these necessary?
	disp_spi.unlock()		#

	disp_cs = board.PIN
	disp_dc = board.PIN
	disp_rst = board.PIN
	
	# ST7796S Display
	DISP_ROTATION = 0  # supported values: 0, 90, 180, 270
	DISP_SPEED = 80000000 # SPI bus clock frequency in Hz. Tested 3.5" display supports 80MHz.
	DISP_WIDTH = 320 if DISPLAY_ROTATION == 0 or DISPLAY_ROTATION == 180 else 480
	DISP_HEIGHT = 480 if DISPLAY_ROTATION == 0 or DISPLAY_ROTATION == 180 else 320
	
	displayio.release_displays()
	disp_bus = displayio.FourWire(
				     disp_spi,
				     command=disp_dc,
				     chip_select=disp_cs,
				     reset=disp_rst,
				     baudrate=DISP_SPEED,
				     phase=0,
				     polarity=0
				    )
	display = ST7796(disp_bus, width=DISP_WIDTH, height=DISP_HEIGHT, rotation=DISP_ROTATION)
	
	# Quick Colors for Labels
	TEXT_BLACK = 0x000000
	TEXT_BLUE = 0x0000FF
	TEXT_CYAN = 0x00FFFF
	TEXT_GRAY = 0x8B8B8B
	TEXT_GREEN = 0x00FF00
	TEXT_LIGHTBLUE = 0x90C7FF
	TEXT_MAGENTA = 0xFF00FF
	TEXT_ORANGE = 0xFFA500
	TEXT_PURPLE = 0x800080
	TEXT_RED = 0xFF0000
	TEXT_WHITE = 0xFFFFFF
	TEXT_YELLOW = 0xFFFF00
	
	# Label Customizations
	hello_label = label.Label(terminalio.FONT)
	hello_label.anchor_point = (0.5, 1.0)
	hello_label.anchored_position = (DISPLAY_WIDTH/2, DISPLAY_HEIGHT/2)
	hello_label.scale = (3)
	hello_label.color = TEXT_WHITE
	
	# Create Display Groups
	text_group = displayio.Group()
	text_group.append(hello_label)
	display.root_group = text_group
	
	while True:
		hello_label.text = "HELLO WORLD!"


Usage Example (CPv9)
====================

.. code-block:: python

    	import board
	import displayio, fourwire # split off into separate module
	import terminalio
	from adafruit_display_text import label
	from circuitpython_st7796s import ST7796S
	
	disp_spi = board.SPI() # OR # import busio;spi = busio.SPI(clock=board.PIN, MISO=board.PIN, MOSI=board.PIN)

	while not disp_spi.try_lock():  #
		pass		   	# Are these necessary?
	disp_spi.unlock()		#

	disp_cs = board.PIN
	disp_dc = board.PIN
	disp_rst = board.PIN
	
	# ST7796S Display
	DISP_ROTATION = 0  # supported values: 0, 90, 180, 270
	DISP_SPEED = 80000000 # SPI bus clock frequency in Hz. Tested 3.5" display supports 80MHz.
	DISP_WIDTH = 320 if DISPLAY_ROTATION == 0 or DISPLAY_ROTATION == 180 else 480
	DISP_HEIGHT = 480 if DISPLAY_ROTATION == 0 or DISPLAY_ROTATION == 180 else 320
	
	displayio.release_displays()
	disp_bus = fourwire.FourWire(
				     disp_spi,
				     command=disp_dc,
				     chip_select=disp_cs,
				     reset=disp_rst,
				     baudrate=DISP_SPEED,
				     phase=0,
				     polarity=0
				    )
	display = ST7796(disp_bus, width=DISP_WIDTH, height=DISP_HEIGHT, rotation=DISP_ROTATION)
	
	# Quick Colors for Labels
	TEXT_BLACK = 0x000000
	TEXT_BLUE = 0x0000FF
	TEXT_CYAN = 0x00FFFF
	TEXT_GRAY = 0x8B8B8B
	TEXT_GREEN = 0x00FF00
	TEXT_LIGHTBLUE = 0x90C7FF
	TEXT_MAGENTA = 0xFF00FF
	TEXT_ORANGE = 0xFFA500
	TEXT_PURPLE = 0x800080
	TEXT_RED = 0xFF0000
	TEXT_WHITE = 0xFFFFFF
	TEXT_YELLOW = 0xFFFF00
	
	# Label Customizations
	hello_label = label.Label(terminalio.FONT)
	hello_label.anchor_point = (0.5, 1.0)
	hello_label.anchored_position = (DISPLAY_WIDTH/2, DISPLAY_HEIGHT/2)
	hello_label.scale = (3)
	hello_label.color = TEXT_WHITE
	
	# Create Display Groups
	text_group = displayio.Group()
	text_group.append(hello_label)
	display.root_group = text_group
	
	while True:
		hello_label.text = "HELLO WORLD!"

Contributing
============

Contributions are welcome! Please read our `Code of Conduct
<https://github.com/DJDevon3/CircuitPython_ST7796/blob/main/CODE_OF_CONDUCT.md>`_
before contributing to help this project stay welcoming.

Documentation
=============

For information on building library documentation, please check out
`this guide <https://learn.adafruit.com/creating-and-sharing-a-circuitpython-library/sharing-our-docs-on-readthedocs#sphinx-5-1>`_.
