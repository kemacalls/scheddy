# scheddy

## description

a tool created to display [couch-to-5k style workout schedules](https://www.c25k.com/c25k_metric.html)
in a couple of different ways. but i'm sure it could be used for other things as well.

#### how does that work

first, you transcribe your schedule in an easy yaml format.  
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

or this table:  

![image](https://i.imgur.com/aGh2ARK.png)

## install

manually:

```
git clone https://github.com/okosuno/scheddy.git 
cd scheddy
pip install -r requirements.txt
```
## execution

simplest usage:

```
chmod +x scheddy
./scheddy [commands]
```

from there you can add it to anywhere you like your binaries    
for me it was `~/.local/bin/` with my other python programs  

```
usage: scheddy [-h] [-m {poly,polym,table}] [-i INTERVAL] [-n] [-c CONFIG]

options:
  -h, --help            show this help message and exit
  -m {poly,polym,table}, --mode {poly,polym,table}
                        choose output style
  -i INTERVAL, --interval INTERVAL
                        time in seconds between lines in polym mode (default:10)
  -n, --no-date         do not show date in tables
  -c CONFIG, --config CONFIG
                        specify alternative path for config
```

use `-i` flag with `poly` or `polym` modes    
use `-n` flag with `table` mode     


## future plans

in no particular order:  

1. more scrolling output options (tomorrow's workout, days elapsed)
2. custom theme/formatting options
3. configure new schedule through commands
4. add tests
