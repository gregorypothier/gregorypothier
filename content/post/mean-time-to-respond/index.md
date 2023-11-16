---
title: Tracking Mean Time to Respond to Detections
subtitle: The fourth part of a four-part technical blog series exploring how to track the mean time to respond to detections.

# Summary for listings and search engines
summary: The fourth part of a four-part technical blog series exploring how to track the mean time to respond to detections.

external_link: https://www.tanium.com/blog/track-mean-time-respond-4-part-blog-series/

# Link this post with a project
projects: []

# Date published
date: '2017-05-03T00:00:00Z'

# Date updated
date: '2017-05-03T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
#   focal_point: ''
#   placement: 1
#   preview_only: false

# authors:
#   - Gregory Pothier

tags:
  - Security

---

# Tracking mean time
How useful would it be to track Mean Time to Patch for every device on your network? What about being able to instantly deliver accurate results about the number of open patches anytime your CIO, CSO, or VP of Ops asks for it?

These were questions we started asking ourselves here at Tanium. The answers hold real business value for our security and IT leaders, who can use the data to monitor our attack surface and patch performance on an ongoing basis.

It’s true that most organizations don’t even know the current status of patches across their network, but at Tanium we not only do this, we also created a metric to track the average time it takes to patch.

This is the single most accurate way we at Tanium use the Tanium Platform to gather metrics on how well our organization is performing patch management. Tanium makes it simple to gather accurate results, such as open critical patches and the state of every installed application, across even the largest enterprise. For CSOs and other security leaders, a snapshot of open patches across the enterprise is a key metric to have, as it helps them assess risk potential. With Tanium, we can look a step further, measuring how well we are patching by gauging the average (mean) time to apply patches across the enterprise. Here’s how we accomplish this, using Tanium and Splunk, a data analytics tool.

Tanium Connect
First, we set up a Tanium Connect that feeds Splunk our Tanium Question “Get Computer Name and Operating System and Available Patches from all machines.” The operating system is optional; we add it in case we ever want to filter results based on specific operating systems in the future.

![patch 1](3-14-17-1.jpg)

With the Connect in Tanium created, we run it and check in Splunk to ensure the results are being processed as expected. We begin the search with the query index=“tanium” because we have configured this connection to be indexed as Tanium. Then, we add the following:

```index=”tanium”```

Question="Get-Computer-Name-and-Computer-Serial-Number-and-Available-Patches-from-all-machines"
This provides all the available patch results listed by computer name. Now we have a list of all patches, including the Title Severity, CVE_ID etc. (Note: We use a table for formatting results in the below screenshot for visual consumption only; this formatting is not otherwise necessary.)

![patch 2](3-14-17-2.jpg)

At this point, we create a nice visual display of patches by severity type. In order to ensure we don’t process duplicate results, we pipe the connect information into a deduplication function such as:

```| dedup Computer_Serial_Number, KB_Article, CVE_ID, Title```

![patch 3](3-14-17-3.jpg)

This ensures these values (Computer_Serial_Number, KB_Article, CVE_ID, Title ) are reported only once and thus are unique. Once we have the unique values, we run a simple function to chart the results by severity:

```| chart count by Severity```

The results create a nice chart illustrating the total counts of each type of severity, as well as the percentage:

![patch 4](3-14-17-4.jpg)

Now we have a solid, automated dashboard of current patches open by severity. Note that we could easily do the same for machines running other operating systems, such as Linux or Mac OSX. Let’s continue with our objective of creating an automated solution which calculates and displays mean time to patch.

Next, we go back to our base query and remove the deduplication so we can work with all of the patch logs which came in. Then we add:

```| stats earliest(_time) as First, latest(_time) as Last by Computer_Name, CVE_ID, Severity, Title```

![patch 5](3-14-17-5.jpg)

This leverages the statistics function to check the first time the patch was reported, as well as the last time the patch was reported, per computer name, CVE_ID, Severity and title. This report provides us with a timestamp of when the patches were first seen and last seen. Now, we take the difference of the two values to see what the duration is, and then convert the epoch time format to a readable string:

```| eval diff = Last - First | eval diff2 = tostring(diff, "duration")```

![patch 6](3-14-17-6.jpg)

The results list the computer name, the patch information, and the amount of time each patch was reported as open on each computer. Now, we calculate the actual maximum, minimum, and mean of those difference values:

```| stats count, max(diff), min(diff), mean(diff)```

And that’s it. We now know the maximum, minimum, and mean values of all patches. We make it pretty by renaming mean(diff) as average, rounding off the extra decimal values, and creating a nicely formatted string showing day hours, minutes, etc.

```| rename mean(diff) as average | eval average = round(average, 0) |eval averageTime=tostring(average,```

![patch 8](3-14-17-7.jpg)

In this blog post, we used one saved Question from Tanium, sent once a day via Tanium Connect into Splunk, to create two important, automated metrics. IT leadership can use this information to measure our attack surface area and patching performance, in current state and over time.