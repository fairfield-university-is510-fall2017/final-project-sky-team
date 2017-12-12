# The Sky Team's Final Project: All About SFO
by Trang Vu & Anthony Iorio

## Background
Using data derived from the City of San Francisco, California and the SFO Airport Commission, the purpose of our analysis is to analyze flight statistics - which include a variety of data, such as airlines, passengers, destinations, prices, and IATA codes. There are so many dimensions to this data, our ERD design needed to be complete enough to account for it all, yet versatile enough to be usuable in a clear(ish) fashion.

### What is ['air-traffic-passenger-statistics'](https://catalog.data.gov/dataset/air-traffic-passenger-statistics)?
Well, nice of you to ask! This is a comma-seperated value file containing the records of over 17,500 rows of data, spanning over 12 years! And that's not even mentioning the diverse range of columns, each adding a unique dimension to interpreting the data. In SFO alone, the airline industry has changed so much over that period of time that there will be plenty of observable trends derived from the metrics gleaned by SFOAC in this databank. There's even many airlines on that list who (sadly) no longer grace our skies...the consolidation of the airline industry from 2009-2015 has really left its mark. We even paired it up (or shall we say...JOINed...) it with another table relating to SFO airport data, which included more detailed information for roughly the same timespan, and included neato features like equipment types (the DC-9 is the best civil aircraft, just sayin'), fleet metrics, and more. We linked to it eternally, which shows we didn't edit the source data...and it was a nice complement to our original dataset.

Here's a little runthrough of the columns, and what they mean:
* **ActivityPeriod** (`ActivityPeriod): This is the month and year of the row you're reading about, which is reflective of the year and month in a YYYYMM format.
* 

As you check out the dataset, keep the following in mind:
* It was originally created on June 16, 2016.
* It was last updated on October 31, 2017.
* If you wish to use the data for other purposes, it is our recommendation that you do the analysis on a period-over-period basis (such as November 2010 vs. November 2011). Don't just take it from us - that's what the city recommends, too. Anyone who knows anything about the airline industry can tell you why: it's better to compare apples-to-apples, and just like many other industries, the airlines have their busy seasons, and they measure their financial and operational performance in relation to each others' seasons.
