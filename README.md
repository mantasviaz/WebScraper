# Web Scraper

## Overview
The scraper is used to collect data points of property data on a widely used real estate platform.

Overview

The Eduscraper command line interface (CLI):

Ingests CSV files of students (with first name, last name, and email)
Uses a long-running process to enrich student data (with school, degree, start year, end year)
Outputs an enriched CSV file
Users

The CLI is designed to be used by teams of one admin user and one or more scraper users. An admin user can also be a power user.

The admin user is responsible for cleaning and partitioning student files to distribute to scraper users. This user should be able to run the CLI on their own computer regardless of setup.

Scraper users are responsible for running the enrichment process. These users have additional hardware, software, and network requirements to perform large-scale enrichment.

Important

Scraper users need to complete the hotspot setup before running the CLI.
Files

Note

Each file should be specific to a single school, and accordingly all emails in a file should share the same school root domain (e.g, @nd.edu).
Input Files

Input files require the following columns in the specified order. Input files can contain the optional columns from the output files.

Name	Type	Description
First Name	string	The student's first name.
Last Name	string	The student's last name.
Email	string	The student's email address.
Output Files

Output files provide the following columns in the specified order.

Name	Type	Description
First Name	string	The student's first name.
Last Name	string	The student's last name.
Email	string	The student's email address.
Search School	string (optional)	The school name used for searching.
Search Keywords	string (optional)	The keywords used for searching.
Result Header	string (optional)	The header of the search result.
Result Preview	string (optional)	The preview text of the search result.
Result URL	string (optional)	The URL of the search result.
School	string (optional)	The name of the student's school.
Degree	string (optional)	The student's degree.
Field	string (optional)	The student's field of study.
Start Year	integer (optional)	The year the student started their degree.
End Year	integer (optional)	The year the student completed their degree.
Status	string (optional)	The student's current enrichment status.
Installation

Get the latest release zip file for your operating system in the team slack.

Download and double click the zip file to extract the executables. The extracted files should include both an eduscraper and an installer executable. Open the installer executable. On MacOS, right click and Open the file. On Windows, double click the file.

Once the installer process completes, close the current terminal, delete the zip and extracted files. The CLI should be installed and accessible from any directory by typing eduscraper in the terminal.

Note

Run eduscraper using the default terminal.

MacOS: Go to Finder > Applications > Utilities > Terminal.
Windows: Go to Start > Run > Terminal.
Usage

Complete the following steps to ingest a student file from a school and enrich it. Start each step by typing eduscraper in the terminal and selecting the desired command.

Step 1: Clean

The admin user can run the clean command to remove non-student accounts from a raw input CSV file.

Provide the path to the raw input CSV file (e.g, ~/Documents/samples/nd.csv) and the desired path to the cleaned input CSV file (e.g, ~/Documents/samples/nd-cleaned.csv).

Step 2: Split

The admin user can run the split command to break a cleaned input CSV file into parts that can be distributed to scraper users.

Provide the path to the cleaned input CSV file (e.g, ~/Documents/samples/nd-cleaned.csv) and the desired number of parts (e.g, 10). This will output part files in the same directory (e.g, ~/Documents/samples/nd-cleaned-1.csv, ~/Documents/samples/nd-cleaned-2.csv, etc.).

Step 3: Load

The scraper users can run the load command to a cleaned part file into their local database.

Provide the path to the cleaned part file (e.g, ~/Documents/samples/nd-cleaned-1.csv).

Step 4: Verify

Optionally, before enriching, the scraper users should run the verify command to verify that their hotspot is configured correctly.

Step 5: Enrich

The scraper users can run the enrich command to enrich their loaded students from a school. This command can be run multiple times (e.g, on consecutive nights) to complete large schools. The enrichment process will resume where it left off.

Provide the name of the school (e.g, University of Notre Dame) and provide a count (e.g, 1000) to cap the number of students to enrich in a run.

Step 6: Download

The scraper users can run the download command to download the current enriched data from a school.

Provide the name of the school (e.g, University of Notre Dame) and the output file path (e.g, ~/Documents/samples/nd-output-1.csv).
