---
description: Documentation for version 2.1 or later
---

# Conditionals

{% hint style="success" %}
[Download this extension](https://bracketspace.com/downloads/notification-conditionals/)
{% endhint %}

## Date comparisons

The `merge tag` and `value` fields can be any ISO-standardized date-time format

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Example of valid date times</p></figcaption></figure>

### Is before/after hour

With this comparison you can check if the date is before or after an hour during the day, using a 24-hour format.

Ie. the date with time **2:12 pm** will produce the following results:

* \<after hour> 14 = ✅
* \<after hour> 13 = ✅
* \<before hour> 14 = ❌
* \<before hour> 15 = ✅

### Is day of week

You can check whether the date is a specific day of the week using numbers 1-7, where:

* Monday - `1`
* Tuesday- `2`
* Wednesday - `3`
* Thursday - `4`
* Friday - `5`
* Saturday - `6`
* Sunday - `7`

You can use multiple values here. If you'd like to check if a date is Monday or the weekend, you'd set the value to: `1,6,7`.

## Is month

Similarly to "Is day of week", you can check if a date is a specific month using numbers 1-12, where:

* January - `1`
* February `2`
* March - `3`
* April - `4`
* May - `5`
* June - `6`
* July - `7`
* August - `8`
* September - `9`
* October - `10`
* November - `11`
* December - `12`

You can use multiple values here. If you'd like to check if a date is the last quarter of the year, you'd set the value to: `10,11,12`.
