#DataTypes
I try to cover the data types.

This document is up to date as of August-2016

###Order/Client ID's

128bit values

Encoded as hexidecimal in the form

      "c687f29d-61dc-4056-8bbb-b5e0fac985e0"

A generalized regex to capture this value

      "([a-f\d-]+)"
      
If you want to capture subfields

      "([a-f\d]{8})-([a-f\d]{4})-([a-f\d]{4})-([a-f\d]{4})-([a-f\d]{12})"
      
###Value Fields

This are the numbers that hold BTC/USD/EUR values. It should be noted there are 2 ways this fields will appear

      null
      "0"
      "502.134123"

The easiest way to "capture" this value is

      (null|"[\d\.]+")
      
When parsing this value into an actual number. I suggest using an `u64`, `uint64_t`, `unsigned long long`. There is a maximum of 12 decimals (or I've seen no fields longer)

      .*(\d{1,6})\.?(\d{1,12})?
      
How to hold this information into a `uint64_t`/`u64` is left as an exercise to the reader.


###Sequence

Each new packet will increase this value by 1. 

Heartbeat messages will contain the value of the previous packet, they will not increment this value.
