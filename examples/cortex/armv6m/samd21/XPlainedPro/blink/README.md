# |=-----=[ Blink example ]=-----=|

## Example
This application is a simple periodic example which toggles the orange led of the board.

Have a look into "blink.oil" file.

The system is based scheduled with a 1ms SysTick "SystemCounter".

The task "blink" toggles the ORANGE (PB.30) led when executed.
This is not scheduled when the program starts.

This task is activated by the alarm `blink\_blink`. The alarm:

 * starts 250ms (`ALARMTIME`) after "StartOS".
 * has a 250ms (`CYCLETIME`) period.

## Build prerequiste

You should have: 

 * A cross-compiler suite: `arm-none-eabi-gcc`
 * [openocd](http://openocd.org/) to flash the board with **` CMSIS-DAP` support**.


## Build

Configure the application with: 

```
goil --target=cortex/armv6m/samd21/XPlainedPro --templates=../../../../../../goil/templates/ blink.oil
```

The `goil` compiler generates the `make.py` [python build script](https://github.com/TrampolineRTOS/trampoline/wiki/Application-Build-system). Then run the script:

```
./make.py all
```

The `blink_exe` should be generated. Then flash the board:

```
openocd -f board/atmel_samd21_xplained_pro.cfg -c "program blink_exe verify reset exit"
```

Note: There is no `make.py flash` at this date, because goil cannot escape the `"` (ticket #20).

## Clean

Use the `clean` target of the make.py:

```
./make.py clean
```