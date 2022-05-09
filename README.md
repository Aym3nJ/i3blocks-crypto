# i3blocks-crypto

![B&W Themed i3blocks-crypto](https://user-images.githubusercontent.com/19287477/35080253-485a4400-fc47-11e7-8ef0-2208869ac822.png)

:dollar: View your favorite coins' ticker prices with i3blocks.

## Setup

![BTC, BCH, ETH i3blocks-crypto](https://user-images.githubusercontent.com/19287477/34461337-9bc48ff4-ee61-11e7-8676-638dd5d1b75b.png)

### Requirements
* i3
* i3bar
* i3blocks
* Python 3. Works on Python 2 as well, just remove the `3` from `#!/usr/bin/env python3` on the top line of the "crypto" script.
  * requests library (`pip3 install requests`)
* (Optional, but recommended) Nerd Font for custom icons (bitcoin's B symbol, bitcoin cash's cash icon, ethereum's diamond icon, or any other icon you want) to display. I'm using Roboto Mono Nerd Font Regular.

### Configurations

1. Ensure the "crypto" script within this repo has execute permission. If unsure, run the following:

    ```sh
    chmod +x crypto
    ```

2. Ensure the `font` attribute within **i3 config** is prefixed with `pango:` for HTML colors to work. If it is already prefixed, skip this step. Example:

    ```
    font pango:RobotoMono Nerd Font Regular 8
    ```

3. Add the following to your **i3blocks config** (3 instances, Bitcoin, Bitcoin Cash and Ethereum). Remember to change the path within the command attribute to point to the "crypto" script.

    ```
    [crypto]
    label=
    markup=pango
    interval=60
    instance=BTCUSDT
    command=~/path/to/i3blocks-crypto/crypto # CHANGE ME

    [crypto]
    label=
    markup=pango
    interval=63
    instance=ETHUSDT
    command=~/path/to/i3blocks-crypto/crypto # CHANGE ME
    ```

## Customization

### Icon

To customize the icon that appears to the left of each ticker, simply change the block's `label` attribute within i3blocks config file (eg. `label=$`). If you are using a Nerd Font, here is a great reference for finding the icon you are looking for: http://nerdfonts.com/#cheat-sheet

### Interval

To customize the interval between each query, simply change the block's `interval` attribute within i3blocks config file (eg. `interval=60` - query every 60 seconds). The interval is block-specific, so each coin can have different query intervals. I chose not to make the intervals the same for each coin to avoid querying them all at once.

### Adding a New Cryptocurrency

Adding a new coin to your i3blocks config is super simple. Use this template within i3blocks config to add a new coin:

```
[crypto]
label=<icon>
markup=pango
interval=60
instance=<coin tag used by Binance>
command=~/path/to/i3blocks-crypto/crypto
```

The "crypto" script uses Binance's free to use API no login needed to query prices. To find out the tag name of the coin you want to add, visit the API's docs for more info (eg. https://binance-docs.github.io/apidocs/spot/en/)

You can add a custom rocket icon as the label as well. First, search "rocket" in http://nerdfonts.com/#cheat-sheet, second, copy the hex value ("f135"), next, paste the hex value into the "hexadecimal" text area in https://r12a.github.io/apps/conversion/, lastly, copy the character output from the "characters" text area and paste it into the `label` attribute.

![XLM crypto i3block](https://user-images.githubusercontent.com/19287477/34461338-9bf60570-ee61-11e7-8217-5ad510b19ffd.png)

### Display Price in BTC

By default the coin values are displayed in USD. Add the argument BTC to the command string to make the output price be displayed in BTC

```
[crypto]
label=$
markup=pango
interval=61
command=~/path/to/i3blocks-crypto/crypto BTCUSDT
```

## Ideas

* Add option to use Bitfinex API instead of CoinMarketCap. Perhaps use any exchange with ccxt
* Trigger something when block is clicked. Open coin's information in web browser, or copy the current price, or open exchange in web browser, etc.
* Add indicator functionality. Alert whenever an indicator has a crossover, SMA? PSAR? etc.

