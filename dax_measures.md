# Elizium Hotels – DAX Measures Documentation

This document contains all key business KPIs and performance measures used in the Elizium Hotels Power BI dashboard.

These measures are used to track revenue, occupancy, pricing, booking performance, and week-on-week trends.

---

## 📊 Core Business Metrics

### Total Bookings
```DAX
1. Total_Bookings := COUNT(Bookings[Booking_ID])

2. Successful_Bookings :=
CALCULATE(
    [Total_Bookings],
    Bookings[Booking_Status] = "Checked Out"
)

3. Total_Cancelled_Bookings :=
CALCULATE(
    [Total_Bookings],
    Bookings[Booking_Status] = "Cancelled"
)


4. Total_No_Show_Bookings :=
CALCULATE(
    [Total_Bookings],
    Bookings[Booking_Status] = "No Show"
)


## Revenue & Pricing Metrics

5. Revenue := SUM(Bookings[Revenue])

6. ADR :=
DIVIDE(
    [Revenue],
    [Total_Checked_Out]
)


7. ADR :=
DIVIDE(
    [Revenue],
    [Total_Checked_Out]
)


8. RevPAR :=
DIVIDE(
    [Revenue],
    [Total_Capacity]
)


9. Realisation % :=
DIVIDE(
    [Revenue],
    SUM(Bookings[Expected_Revenue])
)

## Occupancy & Capacity Metrics

10. Total_Capacity := SUM(Rooms[Total_Rooms])

11. Total_Checked_Out :=
CALCULATE(
    [Total_Bookings],
    Bookings[Booking_Status] = "Checked Out"
)


12. Occupancy % :=
DIVIDE(
    [Total_Checked_Out],
    [Total_Capacity]
)


## Stay & Utilisation Metrics

13. No_of_Days := DISTINCTCOUNT(Date[Date])

14. Length_of_Stay :=
AVERAGE(Bookings[Stay_Duration])

15. DSRN :=
DIVIDE([Total_Capacity], [No_of_Days])

16. DSRN :=
DIVIDE([Total_Capacity], [No_of_Days])

17. DBRN :=
DIVIDE([Total_Checked_Out], [No_of_Days])


18. DURN :=
DIVIDE([Successful_Bookings], [No_of_Days])


## Booking Performance Metrics

19. Booking % by Platform :=
DIVIDE(
    [Total_Bookings],
    CALCULATE([Total_Bookings], ALL(Bookings[Platform]))
)


20. Booking % by Room Class :=
DIVIDE(
    [Total_Bookings],
    CALCULATE([Total_Bookings], ALL(Rooms[Room_Class]))
)

21. Cancellation % :=
DIVIDE(
    [Total_Cancelled_Bookings],
    [Total_Bookings]
)

22. No_Show_Rate % :=
DIVIDE(
    [Total_No_Show_Bookings],
    [Total_Bookings]
)


## Customer Experience Metrics

23. Average_Rating := AVERAGE(Reviews[Rating])

## Week-on-Week (WoW) Change Metrics


24. Revenue_WoW_Change % :=
VAR CurrentWeek = [Revenue]
VAR PreviousWeek =
    CALCULATE(
        [Revenue],
        DATEADD(Date[Date], -7, DAY)
    )
RETURN
DIVIDE(CurrentWeek - PreviousWeek, PreviousWeek)

25 . ADR_WoW_Change % :=
VAR CurrentWeek = [ADR]
VAR PreviousWeek =
    CALCULATE(
        [ADR],
        DATEADD(Date[Date], -7, DAY)
    )
RETURN
DIVIDE(CurrentWeek - PreviousWeek, PreviousWeek)

26. Occupancy_WoW_Change % :=
VAR CurrentWeek = [Occupancy %]
VAR PreviousWeek =
    CALCULATE(
        [Occupancy %],
        DATEADD(Date[Date], -7, DAY)
    )
RETURN
DIVIDE(CurrentWeek - PreviousWeek, PreviousWeek)

27. RevPAR_WoW_Change % :=
VAR CurrentWeek = [RevPAR]
VAR PreviousWeek =
    CALCULATE(
        [RevPAR],
        DATEADD(Date[Date], -7, DAY)
    )
RETURN
DIVIDE(CurrentWeek - PreviousWeek, PreviousWeek)


28. Realisation_WoW_Change % :=
VAR CurrentWeek = [Realisation %]
VAR PreviousWeek =
    CALCULATE(
        [Realisation %],
        DATEADD(Date[Date], -7, DAY)
    )
RETURN
DIVIDE(CurrentWeek - PreviousWeek, PreviousWeek)


## Summary

These measures power the full Elizium Hotels analytics dashboard including:

Revenue & pricing analytics

Occupancy & utilisation tracking

Booking platform & room class analysis

Cancellation & no-show monitoring

Week-on-week business performance

They enable hotel management to make data-driven pricing, marketing, and capacity planning decisions.


