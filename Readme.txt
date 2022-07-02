# LIRC conf files for Volvo RTI Remotes

This repo is a sideproduct of this blog article: https://blog.julian-lemmerich.de/220701-volvoir.html

## Usage

Copy it to `/etc/lirc/lircd.conf.d/` and reboot. You might also remove the default `devinputs.conf` file.

```
sudo cp ./Volvo30657371-1.lircd.conf /etc/lirc/lircd.conf.d/Volvo30657371-1.lircd.conf
sudo mv /etc/lirc/lircd.conf.d/devinput.lircd.conf /etc/lirc/lircd.conf.d/devinput.lircd.conf.dist
```

## Recording Procedure

Since `irrecord` did not work, this config was created manually.

```
# for every button
sudo mode2 -m -d /dev/lirc0 > Volvo30657371-1_back.log
```

The `.lircd.conf` sceleton is as follows:

```
begin remote

  name   volvo
  flags RAW_CODES
  eps            25
  aeps          100

  ptrail          0
  repeat     0     0
  gap    20921


  begin raw_codes

    name BUTTON_NAME
     8996     4451      552      574      551      576
      552      576      551      579      550      575
      553     1683      577      550      551     1683
      ...
      564

  end raw_codes
end remote
```

The numbers under the name are the blocks of numbers taken from mode2. The last number from the block can be ignored.

Linux has standardised Button names. To display all the buttons your kernel supports, run

```
irrecord -l
```

Using these standard buttons, makes it poosible to later use them as keyboard input.
