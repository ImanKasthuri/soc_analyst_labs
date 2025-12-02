# BTLO Bruteforce

## Overview

## Tools Used

## Question 1) How many Audit Failure events are there?
I used PowerShell to gather Audit Failure events using this commands.

1. $log = Import-Csv "BTLO_Bruteforce_Challenge.csv"

The above command is used to load CSV file in to PowerShell.

2. $log | Where-Object { $_.keywords -eq "Audit Failure" } | Measure-Object

This command is used to filtor, how many failed audit are there.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bb3ab58f-c024-4541-a7ab-1fd92e513637" />







