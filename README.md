Plaintext Accounting for Weight Loss
------------------------------------

This project uses Ledger-CLI to keep track of calories.

My process is to measure and record everything I eat, and any
exercises I do, on little scraps of paper then transcribe them into a
ledger and report on that later.

I also weigh myself once a day and record that in the ledger.

This isn't the most convenient way to count calories.  Measuring and
recording everything is time consuming and tedious.

There are programs and apps designed especially for this purpose.
They make the process less of a chore, but let's face it, it's always
a chore.

Fortunately, watching one's weight is all about learning to pay
attention.  Developing better eating habits should come naturally if
the process is executed in earnest.

After a while, it should be possible to "coast" and maintain a desired
weight without all the bookkeeping.  When that stops working (and it
will), start again to get it back under control.

Benefits of Using a Ledger
--------------------------

This ledger tracks foods and exercises per unit.  Some examples:

    P 2000-01-01 12:00:00 g_beans_black   1.320 cal
    P 2000-01-01 12:00:00 floz_wine_red  25.000 cal

Black beans are 1.320 calories per gram.  Red wine is 25 calories per
fluid ounce.

Thinking of foods in terms of caloric "density" (calories per unit)
lets someone make "apples to apples" comparisons among their options.

For example, apples are about 0.520 calories per gram.  If protein
isn't a concern, one can fit twice as much apple as beans in one's
diet for the same calorie cost.

Biology
-------

Side note.  Biology.  Humans are made of it.  We have a biological
need to consume and store energy in times of abundance so we have them
on-hand (or on-hip) in times of scarcity.

To help us do that, we have a tendency to use our calories
efficiently, and we find the densest concentrations of calories are
the most delicious and desirable.

No talk of human biology would be responsible without mentioning
irregular ones.  If your biology is out-of-whack, see a doctor before
trying diets you've read about on the Internet.

For healthy people, the big problem is there's no scarcity in modern
consumer-driven societies.  Calories are readily available as long as
one has the means to purchase them.  The most desirable calories are
marketed the heaviest since they can be the most profitable.

So we have to be mindful of what we're eating and exercise control
over it.

Losing Weight is Like Saving Money in Reverse
---------------------------------------------

I'm told losing weight is easy.  All I have to do is burn more
calories than I consume.

    my net calories += what I ingest - what I expend

I'm told saving money is easy.  All I have to do is spend less money
than I earn.

    my net cash += what I earn - what I spend

The goals are opposite, but the processes are nearly identical.

Given that, it's not a huge stretch to use a ledger to keep track of
my fat assets.

About the Files
---------------

This system comprises four files:

basal.prices - People burn calories just by being alive.  This include
file estimates how many calories I burn on a normal day.

exercise.prices - Unit price database for various forms of exertion.

food.prices - Unit prices database for different kinds of foods.

calories.ledger - The ledger itself.

About the Ledger
----------------

The ledger consists of three kinds of entry:

1. Includes.  These pull in the various databases.

    include basal.prices
    include food.prices
    include exercise.prices

2. Basal metabolism transactions.  These account for being alive.  They contain two postings: One line to calculate your basal burn from your weight, and another line to offset that burn from "Assets:Fat".

    2016-10-27 Sedentary Metabolism
      Assets:Fat
      Espenses:Basal:Weight  190.000 lb_basal_weight

3. Exercise transactions.  These track events that burn extra calories.  The "exercise.prices" database converts units of exercise into calories burned, and the "Assets:Fat" offset is calculated to match.

    2016-10-27 Housecleaning
      Assets:Fat
      Espenses:Housecleaning   30 min_vacuuming
      Espenses:Housecleaning   60 min_housecleaning_light

4. Meal transactions.  The food.prices database converts food measurements into calories, and the "Assets:Fat" offset is calculated to match.

```
    2016-10-27 Breakfast
      Assets:Fat
      Income:Breakfast  -30 g_raisin_bran
      Income:Breakfast  -20 g_walnuts
    2016-10-27 Breakfast Coffee
      Assets:Fat
      Income:Coffee      -6 g_sugar_turbinado
      Income:Coffee      -2 g_cocoa
      Income:Coffee    -328 g_coffee
      Income:Coffee    -108 g_milk_twopct
    2016-10-27 Lunch
      Assets:Fat
      Income:Lunch      -10 g_butter
      Income:Lunch       -1 bagel_thomas_cinnamon_raisin
      Income:Lunch      -14 g_oats_dry
      Income:Lunch      -20 g_nuts_mixed_planters
      Income:Lunch       -1 g_honey
    2016-10-27 Lunch Coffee
      Assets:Fat
      Income:Coffee      -6 g_sugar_turbinado
      Income:Coffee      -2 g_cocoa
      Income:Coffee    -304 g_coffee
      Income:Coffee    -114 g_milk_twopct
    2016-10-27 Dinner
      Assets:Fat
      Income:Dinner     -83 g_beef_bottom_round_roasted
      Income:Dinner     -76 g_beans_green
      Income:Dinner     -50 g_carrots_raw
      Income:Dinner     -77 g_onions_sauteed
      Income:Dinner    -145 g_potatoes_steamed
      Income:Dinner     -21 g_lingonberries
    2016-10-27 Dessert
      Assets:Fat
      Income:Dessert    -31 g_graham_crackers_honey
```

Daily Report
------------

A daily value report on Assets will describe the gain/loss for each
day.  More importantly, the balance will tell whether progress is
being made overall.  It's okay to have bad days as long as the overall
trend is in the right direction.

    % ledger --value -f calories.ledger reg Assets --daily
    16-Oct-27 - 16-Oct-27  Assets:Fat    -320.370 cal   -320.370 cal
    16-Oct-28 - 16-Oct-28  Assets:Fat    -119.632 cal   -440.002 cal
    16-Oct-29 - 16-Oct-29  Assets:Fat    -455.513 cal   -895.515 cal
    16-Oct-30 - 16-Oct-30  <Adjustment>    -0.001 cal   -895.516 cal
                           Assets:Fat    -449.450 cal  -1344.966 cal
    16-Oct-31 - 16-Oct-31  Assets:Fat     197.896 cal  -1147.070 cal
    16-Nov-01 - 16-Nov-01  <Adjustment>     0.001 cal  -1147.069 cal
                           Assets:Fat     -34.909 cal  -1181.978 cal
    16-Nov-02 - 16-Nov-02  Assets:Fat    -250.414 cal  -1432.392 cal

Motivation
----------

The motivation for tracking calories at all came from The Hacker's
Diet.  https://www.fourmilab.ch/hackdiet/

License
-------

Public domain.  It helps me.  I hope it helps someone else, too.

To-Do
-----

basal.prices is tuned for the author.  If you're not exactly the same
as him, you'll need to edit basal.prices.  This will be fiddly for
men, but the basal formula for women is even more different.  If
someone makes basal.prices more generic, or if someone documents the
process they used to modify it, I would totally love to include those
changes.

food.prices and exercise.prices only include things I've needed.  They
could benefit from more varied input, although it may slow down ledger
reports.  We might want to keep a main database of everything and a
separate "include" database for personal use.
