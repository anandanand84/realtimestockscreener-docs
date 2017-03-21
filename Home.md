This is an editor tool which is used to write your own custom screener to find stock matching your trading criteria.

## What programming language is this and how should I write?

Javascript. You request metadata and variables(discussed below) needed using comments at the begining in a specified syntax and write javascript to perform screens and return boolean true if matched. Your screener will be executed for everytick (if run everytick is specified) for every stocks.


## How should I get the required data for my screener and what is the syntax for getting data.


Below is the steps and syntax to get the required data.

### Define a runtype. Run types specify how frequent the screener will be executed to get results (Mandatory)

Syntax :

```
\\RunEveryTick
```

| Keyword      | Description                                                               |
|--------------|---------------------------------------------------------------------------|
| RunEveryTick | Whenever a new trade happens                                              |
| RunOnNewBar  | Whenever a new bar(1 minute) is created                                   |
| RunOnce      | Run once for all scrip to find matching scrip (currently not implemented) |
| RunEOD       | Run only once when the market closes                                      |


### Define a name (Mandatory)

Syntax :

```
\\use name=[word]
```

Word cannot have spaces


### Get Series of data. (Optional but alteast one of series or data)

Array of data based on interval or eod.

Syntax.

```
\\use [number] bars of [number]min [series,] prefixed [word]
```
where number is any Integer, series is the type of values ex:open, high, low, close, timestamp, volume, cumvolume

Example :

```
\\use 10 bars of 5min open
```

Gives you an array[10] with variable name open containing the latest values at index 0. Assuming you imported this below is how your code will be executed.

```
function(open : Array) {
	\\ your code
}
```

```
\\use 5 bars of 2min open,high,low,close
```

Gives you an multiple array[5] with variable names open, high, low, close containing the latest values at index 0.

```
\\use 20 bars of 15min close, timestamp prefixed fifteenMinute_
\\use 5 bars of 2min close, timestamp prefixed twoMinute_
```
Gives you multiple arrays with variable names fifteenMinute_close, fifteenMinute_timestamp(epoch timestamp), twoMinute_close, twoMinute_timestamp


### Get data (Optional but alteast one of series or data)

```
\\use [data,]
```

where data is one or comma sperated below values

| Data    | Description                                   |
|------------|-----------------------------------------------|
| yopen      | Yesterdays open price                         |
| yhigh      | Yesterdays high price                         |
| ylow       | Yesterdays low price                          |
| yvolume    | Yesterdays volume                             |
| ychange    | Yesterdays change value from its previous day |
| ypchange   | Yesterdays percent change                     |
| lastopen   | Todays (currentdays) open                     |
| lasthigh   | Todays (currentdays) high                     |
| lastlow    | Todays (currentdays) low                      |
| lastvolume | Todays volume                                 |
| change     | Todays change                                 |
| pchange    | Todays percent change                         |


### Filters

Filters scrip based on conditions before executing the screener.

Below filter filters the stocks that are in the top 10 turnover list.


```
\\filter topturnover min rank 0 max rank 10
```
