---
title: 'Welcome to PiWeatherRock'
linkTitle: "Documentation"
weight: 20
menu:
  main:
    weight: 20
---

{{% alert title="Notice" color="warning" %}}
On March 30, 2020 an announcement was posted to the [Dark Sky Blog](https://blog.darksky.net) stating that they have
been acquired by Apple. The announcement went on to say that they are no longer accepting new requests for API access and that they
will be shutting the API down at the end of 2021.

This unfortunate bit of news isn't the end of this project... I've been here before. This just means that I will have to do a third
API migration. Work related to this, and suggestions on what API to use, are being tracked in
[issue 48](https://github.com/genebean/PiWeatherRock/issues/48) of the project's GitHub repo.
{{% /alert %}}

PiWeatherRock has three screens that it cycles through to show you a daily forecast, a hourly forecast, and an information screen. Here are examples of each:

| Daily forecast                                         | Hourly forecast                                          | Info screen                                 |
|--------------------------------------------------------|----------------------------------------------------------|---------------------------------------------|
| ![daily-forecast-screenshot](us-daily.png) | ![hourly-forecast-screenshot](us-hourly.png) | ![info-screenshot](us-info.png) |

Data for these forecasts is pulled from Dark Sky via their free API.

## Ready to get started?

Find out how to install PiWeatherRock in [Getting Started](getting-started/).
