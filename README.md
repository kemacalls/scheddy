# scheddy

## description

a tool created to display current progress in [couch-to-5k style workout schedules](https://www.c25k.com/c25k_metric.html) either by printing to terminal or using [polybar](https://github.com/polybar/polybar).

#### how does that work

first, you transcribe your schedule into an easy yaml format.  
then, you can use scheddy for:
  1. updates in polybar about what today's workout looks like
  2. a pretty table printed to terminal detailing your schedule
and scheddy will update hourly without need for refreshing  

## examples

this yaml file:

```yaml
start_date: "06-26-2022"
start_dow: "sun"
week_1:
    dw1: "5W, 1J/1.5W -> 20min"
    dw2: "stretch or core"
    dw3: "5W, 1J/1.5W -> 20min"
    dw4: "stretch or core"
    dw5: "5W, 1J/1.5W -> 20min"
    dw6: "stretch or core"
    dw7: "stretch"
week_2:
    dw1: "5W, 1.5J/2W -> 20min"
    dw2: "stretch or core"
    dw3: "5W, 1.5J/2W -> 20min"
    dw4: "stretch or core"
    dw5: "5W, 1.5J/2W -> 20min"
    dw6: "stretch or core"
    dw7: "stretch"
```

might yield this polybar output:  

`sunday's workout: 5w, 1j/1.5w -> 20min`

or this polybar scrolling output:  

```
sunday, june 26: day 1 of week 1
today's workout: 5W, 1J/1.5W -> 20min
```

or this table (depends on your terminals color scheme):  

![image](https://i.imgur.com/aGh2ARK.png)

## install

manually:

```
git clone https://github.com/okosuno/scheddy.git 
cd scheddy
pip install -r requirements.txt
```
## usage

simplest usage:

```
python scheddy [commands]
```
or  
```
chmod +x scheddy
./scheddy [commands]
```

unless you specify a `--config` path, scheddy will create one at:   
`$HOME/.config/scheddy/`  
and if you don't have a `scheddy.yaml` in your config folder,   
scheddy will make one for you.   

now you can add scheddy's binary to anywhere you like your binaries.    
for me it was `~/.local/bin/` with my other python programs.    

help:  
```
usage: scheddy [-h] [-m {poly,polym,table}] [-i INTERVAL] [-n] [-c CONFIG] [-s STRING] [-l]

options:
  -h, --help            show this help message and exit
  -m {poly,polym,table}, --mode {poly,polym,table}
                        choose output style
  -i INTERVAL, --interval INTERVAL
                        time in seconds between lines in polym mode (default:10)
  -n, --no-date         do not show date in tables
  -c CONFIG, --config CONFIG
                        specify alternative path for config
  -s STRING, --string STRING
                        customize the string for polybar, takes strftime for dates
  -l, --lower           forces given string to be all lowercase
```

use `-i, -s, -l` flags with `poly` or `polym` modes.    
use `-n` flag with `table` mode.     

e.g. `scheddy -m poly -s '%A's workout: ` -l`

here is my polybar module:
```
[module/scheddy]
type = custom/script
exec = /usr/bin/python /home/oko/.local/bin/scheddy -m poly
tail = true
label = " %output% "
label-foreground = ${color.background}
label-background = ${color.shade2}
```

## future plans

in no particular order:  

1. more scrolling output options (tomorrow's workout, days elapsed)
2. custom theme/formatting options
3. configure new schedule through commands
4. __add tests__
5. remove need for "start_dow"
6. __infinite schedule mode -> repeat final week indefinitely__
7. print hypothetical schedules (dateless)
