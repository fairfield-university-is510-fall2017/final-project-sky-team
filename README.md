# The Sky Team's Final Project: All About SFO
by Trang Vu & Anthony Iorio

## Background
Using data derived from the City of San Francisco, California and the SFO Airport Commission, the purpose of our analysis is to analyze flight statistics - which include a variety of data, such as airlines, passengers, destinations, prices, and IATA codes. There are so many dimensions to this data, our ERD design needed to be complete enough to account for it all, yet versatile enough to be usuable in a clear(ish) fashion.

### What is ['air-traffic-passenger-statistics'](https://catalog.data.gov/dataset/air-traffic-passenger-statistics)?
Well, nice of you to ask! This is a comma-seperated value file containing the records of over 17,500 rows of data, spanning over 12 years! And that's not even mentioning the diverse range of columns, each adding a unique dimension to interpreting the data. In SFO alone, the airline industry has changed so much over that period of time that there will be plenty of observable trends derived from the metrics gleaned by SFOAC in this databank. There's even many airlines on that list who (sadly) no longer grace our skies...the consolidation of the airline industry from 2009-2015 has really left its mark. We even paired it up (or shall we say...JOINed...) it with another table relating to SFO airport data, which included more detailed information for roughly the same timespan, and included neato features like equipment types (the DC-9 is the best civil aircraft, just sayin'), fleet metrics, and more. We linked to it eternally, which shows we didn't edit the source data...and it was a nice complement to our original dataset.

Here's a little runthrough of the columns, and what they mean:
* **ActivityPeriod** (`ActivityPeriod`): This is the month and year of the row you're reading about, which is reflective of the year and month in a YYYYMM format.
* **OperatingAirline** (`OperatingAirline`): This is the airline that actually _operated_ the flight. This gets significant later on, and is especially important if you're looking for codeshare flights. (For example, Delta DL5643 is operated by (EV) ExpressJet Airlines on behalf of (DL) Delta Air Lines, using ExpressJet's equipment. Even though it's a flight you can book at Delta.com and Delta sells, it's actually operated by one of Delta Connection's regional partners.)
* **OperatingAirlineIATACode** (`OperatingAirlineIATACode`): The de facto standards and trade organization of the world's airlines, the International Air Transport Association (or IATA for short), assigns a two-letter code to each of the world's airlines. For example, Delta Air Lines is DL, Northwest Airlines is NW, and Air Canada's is AC. Sometimes, they seem random - and they very well could be! Check out Southwest Airlines, which famously has IATA code WN. Since SW was originally taken by Air Namibia, rumor has it they were asked if they wanted a random code. They allegedly responded "Why Not," and WN was born! (Other, less-complimentary versions of that story attribute the WN to "We're Nuts," but that could just be sour grapes. Southwest is a highly successful airline, after all. It could have also had to do with "WIN," as you can't spell WIN without WN.)
* **PublishedAirline** (`PublishedAirline`): This column designates the name of the airline that is the _published_ airline for the flight - which could mean that said airline is not actually the operator. For example, Atlantic Southeast Airlines (ASA) is a regional affiliate of Delta Connection, and ASA-operated flights use he Delta name as their PublishedAirline. That's because they're operating the flight on Delta's behalf!
* **GEOSummary** (`GEOSummary`): This is the general classification of the geographic flight type, such as "Domestic" or "International."
* **GEORegion** (`GEORegion`): This is the specific geographic region the flight was destined for, usually expressed by country.
* **ActivityTypeCode** (`ActivityTypeCode`): This is the column that keeps the primary purpose of the flight as it relates to SFO in the table. There are three classifications: "Deplaned," "Enplaned," and "Thru / Transit." This explains whether the flight *originated* in SFO (Enplaned), was *destined* for SFO (Deplaned), or was simply *connecting/stopping* in SFO and continuing to a final destination elsewhere (Thru / Transit).
* **PriceCategoryCode** (`PriceCategoryCode`): This column keeps track of the classification of the primary fare class of each flight. For example, pretty much all Spirit Airlines-operated flights would be regarded as "Low Fare" (but you really should fly Spirit, don't let that stop you. It's a great value if you know how to book!).
* **Terminal** (`Terminal`): The terminal the flight used. Makes sense, right?
* **BoardingArea** (`BoardingArea`): This is the specific letter-assigned zone that the flight utilized at SFO to conduct boarding operations.
* **PassengerCount** (`PassengerCount`): This is the count of the passengers who were participants in each flight!

As you check out the dataset, keep the following in mind:
* It was originally created on June 16, 2016.
* It was last updated on October 31, 2017.
* If you wish to use the data for other purposes, it is our recommendation that you do the analysis on a period-over-period basis (such as November 2010 vs. November 2011). Don't just take it from us - that's what the city recommends, too. Anyone who knows anything about the airline industry can tell you why: it's better to compare apples-to-apples, and just like many other industries, the airlines have their busy seasons, and they measure their financial and operational performance in relation to each others' seasons.

## Analysis
Having the data is one thing, but utilizing it to extract useful, informative trends is another. We performed an analysis centering on the following concepts outlined below, with a brief description of what we found below them. For the full details, we encourage you to view the full report!

### What did we analyze?
We set out to perform the following operations with the data:
* Organizing key, mission-critical aspects of the data into tables and DataFrames using SQL.
* Analyzing terminal usage metrics.
* Determining the number of passengers throughout the duration of this dataset who participated in each of the `ActivityTypeCode`s.
* Examining passenger metrics to see if a pattern exists among seasonal capacity of flights at SFO.
* Considering the geographic dimensions of passenger activity.
* Observing the fleet composition of carriers included in the dataset.
* Observing the diversity of equipment types that frequent SFO.
* Organizing the number of landings on a carrier-by-carrier basis in a DataFrame.

## Takeaways
As is always the case, we learned a lot from completing this project - and we don't exclusively mean that in a SQLish or Pythonic context. As a two-person group, here were our takeaways!
* **Once again - Google really *IS* your friend.** We've said it before, and we'll say it again: there really is no error message that you'll encounter that someone else has not already also encountered (unless you just have *terrible* luck). At any rate, Google often leads to Stackoverflow, which often leads to solutions to problems. And solutions are a very good thing indeed. So make sure your search engine skills are primed - you'll likely need them!
* **Having an error specialist is a very good thing indeed.** Not to sound too repetitive, but in the last project, we extolled the worth of having a diagnostician who knows what they're doing. In this group, that was clearly Trang. She is a very gifted programmer and excellent person to go to if you encounter an error. Her spotting of problems in a line of code is uncanny! Every group should have someone like Trang if they wish to expedite error resolution - and we all know there *will* be errors.
* **Synchronize your schedules.** We had more git clashes on this project than the last one, and resolving such conflicts wasn't fun (and was likely not helped by GitHub Desktop, which may have malfunctioned, thus compounding the problem). So we either arranged to code together, in person, from one machine in order to avoid these issues. Another thing we did was create our own workspaces (which we later removed), where we could commit as much as we wanted without having to worry about conflicts. So either plan ahead, or get some space for yourselves! It'll make the project a lot less stressful. And while we're on the subject...
* **Panic helps nobody.** As Anthony will tell you, extended periods of social isolation, little sustinence, and very meager sleep are the *perfect* breeding ground for feelings of desperation and hopelessness. He maintains that one of the most torturous things in life is not knowing how to do something in code, or run into an error that seems ambiguous. Such failures threaten the completion of the project not because they are insurmountable, but because they are demoralizing - and it takes an enduring sense of tranquility and perspective to persevere, and get it done! We did it, and it was a team effort...so panic was not necessary. Just don't stress out!
