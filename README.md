# Splunk Lab - Splunk Intro: Perform a query with Splunk

## Overview
In this activity, you'll be introduced to the Splunk platform. Then, you'll use Splunk Cloud to upload data, perform basic searches on the data, and answer a series of questions. Follow the instructions in the <a href="https://www.coursera.org/learn/detection-and-response/supplement/Wg478/follow-along-guide-for-splunk-sign-up">Follow-along guide for Splunk sign-up</a> to complete the following before you begin using Splunk:
  * Create a Splunk account
  * Activate a free trial of Splunk Cloud
  * Upload data into Splunk Cloud

So far, you've learned that SIEM tools, such as Splunk, are an important part of a security analyst's toolbox because they provide a platform for storing, analyzing, and reporting on data from different sources. You also explored some basic searches using Splunk's querying language, called Search Processing Language (SPL), which included the use of pipes and wildcards.

Creating effective searches is an important skill because it enables you to quickly and accurately find the information you are looking for within a large amount of data. Quick and accurate searching is especially useful during incident response, because you might need to swiftly identify and address a security incident. Effective search techniques also help you efficiently identify patterns, trends, and anomalies within data.

## Project Description

You are a security analyst working at the e-commerce store Buttercup Games. You've been tasked with identifying whether there are any possible security issues with the mail server. To do so, you must explore any failed SSH logins for the root account.

This lab demonstrates how Splunk Cloud and its querying language (SPL) can be used by security analysts to investigate potential security incidents by analyzing logs and events from various sources.

## Tools
  * **Splunk Cloud:** A cloud-based Security Information and Event Management (SIEM) tool used for ingesting, analyzing, and reporting on security data from various sources.
  * **Splunk Search Processing Language (SPL):** A query language used to search and analyze data within Splunk.

How the tools were used in this lab:
  * **Splunk Cloud:**
    * **Data Upload:** The lab instructed users to upload a sample data file containing log events from Buttercup Games' mail server and web applications.
    * **Search and Analysis:** Users performed queries using SPL to:
      * Verify data ingestion and searchability.
      * Identify different data sources based on fields like host, source, and sourcetype.
      * Narrow search results to specific hosts and events (e.g., failed SSH login attempts for the root user on the mail server).
      * Analyze search results to answer questions about security incidents.
  * **Splunk Search Processing Language (SPL):**
    * Users employed SPL syntax to construct queries that targeted specific data elements and narrowed the search scope.
    * **Examples of SPL queries used:**
      * index="main": Searches for events within the "main" index.
      * index="main" host=mailsv: Filters results to events originating from the "mailsv" host (mail server).
      * index="main" host=mailsv fail* root: Searches for events with "fail*" (wildcard for failure-related terms) and "root" within the mail server logs.

## Steps
### Task 1. Access supporting material
The following supporting materials will help you complete this activity. The data contains log and event information from Buttercup Games' mail servers and web accounts. This includes information like access and authentication logs, email logs, and more.

To download this data, click the link then click the download icon.
  * **Link to supporting materials:** <a href="https://drive.google.com/file/d/1nDz_DZB4ADbD4tvaDa54_l1FoT_jtVy4/view?usp=share_link">tutorialdata.zip</a> file.

### Task 2. Upload data into Splunk
To operate effectively, it's essential that SIEM tools ingest and index data. SIEM tools collect and process data so that it becomes searchable events that can be queried, viewed, and analyzed.

So far, you've created a Splunk account and activated and accessed the Splunk Cloud free trial, but your Splunk Cloud instance does not contain any data. Next, you'll need to upload data into Splunk to start querying. Complete the following steps to upload data into Splunk:
  * Navigate to Splunk Home from your Splunk Cloud free trial instance. You might need to log in again using your credentials.
  * Upload the tutorialdata.zip file, and click Open.
  * Click the Next button to continue to Input Settings.
  * By the Host section, select Segment in path and enter 1 as the segment number.
  * Click the Review button and review the details of the upload before you submit. The details should be as follows:
    * **Input Type:** Uploaded File
    * **File Name:** tutorialdata.zip
    * **Source Type:** Automatic
    * **Host:** Source path segment number: 1
    * **Index:** Default
  * Click Submit. Once Splunk has ingested the data, you will receive confirmation that the file was successfully uploaded.

### Task 3. Perform a basic search
Take a moment to examine the Splunk Cloud interface by locating the app panel, the Explore Splunk panel, and the Splunk bar.
  * Now that you've uploaded the data into Splunk, perform your first query to confirm that the data has been ingested, indexed, and is searchable. Follow these steps to perform a query:
    * Navigate to Splunk Home. (To return to Splunk Home, click the Splunk Cloud logo on the Splunk Cloud page.)
    * Click Search & Reporting. You may close any pop ups that appear.
    * In the search bar,  enter your search query:
      * index="main"
      * This search term specifies the index. An index is a repository for data. Here, the index is a single dataset containing events from an index named main.
    * Select All Time from the time range dropdown to search for all the events across all time.
    * Click the search button. Note that the search button is represented by the magnifying glass icon. Your search should retrieve thousands of events.
      * ![Splunk 1](https://github.com/user-attachments/assets/cc228d62-496e-4083-a1d7-a405180bb04e)

### Task 4: Now that you've run your first query:
  * Examine the search results and the fields.
    * For each event the fields are host, source, and sourcetype. Under SELECTED FIELDS, examine the same fields.
      * ![Splunk 2](https://github.com/user-attachments/assets/a8c3bd14-0055-42f6-ac2a-a9dad648e0a7)
  * Examine the field values by clicking on the field under SELECTED FIELDS. You should observe the following:
    * **host:** The host field specifies the name of the network host from which the event originated. In this search there are five hosts:
      * mailsv - Buttercup Games' mail server. Examine events generated from this host.
        * www1 - This is one of Buttercup Games' web applications.
        * www2 - This is one of Buttercup Games' web applications.
        * www3 - This is one of Buttercup Games' web applications.
        * vendor_sales - Information about Buttercup Games' retail sales.
      * source: The source field indicates the file name from which the event originates. You should identify eight sources. Notice /mailsv/secure.log, which is a log file that contains information related to authentication and authorization attempts on the mail server.
      * sourcetype: The sourcetype determines how data is formatted. You should observe three sourcetypes. Examine secure-2.

### Task 5: Narrow Your Search
Because you've been tasked with exploring any failed SSH logins for the root account on the mail server, you'll need to narrow the search results for events from the mail server.
  * Under SELECTED FIELDS, click host and click mailsv.
  * Notice that a new term has been added to the search bar:
    * index=main host=mailsv.
    * The search results have narrowed to over 9000 events that are generated by the mail server.
      * ![Splunk 3](https://github.com/user-attachments/assets/e8998581-fcbd-4672-83e5-c415dbd30b55)

### Task 6: Search For A Failed Login For Root
Now that you've narrowed your search results to events generated by the mail server, continue to narrow the search to locate any failed SSH logins for the root account. 
  * Enter index=main host=mailsv fail* root into the search bar.
    * This search expands on the search from the previous task and searches for the keyword fail*. The wildcard tells Splunk to expand the search term to find other terms that contain the word fail such as failure, failed, etc. Lastly, the keyword root searches for any event that contains the term root.
    * ![Splunk 4](https://github.com/user-attachments/assets/688a7f04-987d-4b88-a820-8ca8d0381b34)

### Task 7: Evaluate the search results
  * **How many events are contained in the main index across all time?**
    * *Entering a search for all events in the main index retrieves 109,864 events.*
  * **Which field identifies the name of a network device or system from which an event originates?**
    * *The 'host' field specifies the name of a host, such as a network device or other system, from which an event originates.*
  * **Which of the following hosts used by Buttercup Games contains log information relevant to financial transactions?**
    * *The 'vendor_sales' host provides information about Buttercup Games' retail sales, such as the number of products sold.*
  * **How many failed SSH logins are there for the root account on the mail server?**
    * *There are over 100 failed SSH logins for the root account on the mail server.*

## Summary: Investigating Failed SSH Logins with Splunk Cloud
This activity introduced the Splunk Cloud platform as a powerful tool for security analysts. By creating a free trial account and uploading sample log data, users learned how to:
  * **Perform Basic Searches:** Query the indexed data to identify specific events, such as failed SSH login attempts.
  * **Understand Data Fields:** Recognize the significance of fields like host, source, and sourcetype in categorizing and filtering events.
  * **Narrow Search Results:** Utilize advanced search techniques, such as wildcards and field filtering, to refine search queries.
  * **Analyze Search Results:** Interpret the results of Splunk searches to identify potential security incidents and anomalies.

Through these exercises, users gained practical experience in using Splunk to investigate security events and make informed decisions.
