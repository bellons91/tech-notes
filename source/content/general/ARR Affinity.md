---
title: "ARR Affinity"
tags:
  - arr
  - iis
  - load-balancing
  - azure
  - session-affinity
aliases:
  - Application Request Routing Affinity
---

Application Request Routing (ARR) for IIS 7 and above is a proxy-based routing module that forwards #HTTP requests to application servers based on HTTP headers, server variables, and load-balancing algorithms.

ARR can identify a client by assigning an **affinity cookie**, so subsequent requests from that client are routed to the same backend instance. That keeps session state sticky to one server until the session expires or the [[cookie]] is cleared.

[Configure ARRAffinity cookie when accessing Azure App Service behind Azure Application Gateway](https://techcommunity.microsoft.com/t5/apps-on-azure-blog/configure-arraffinity-cookie-when-accessing-azure-app-service/ba-p/3842511)
[Disable Session affinity cookie (ARR cookie) for Azure web apps](<https://azure.github.io/AppService/2016/05/16/Disable-Session-affinity-cookie-(ARR-cookie)-for-Azure-web-apps.html>)

[Application Request Routing Version 2 Overview](https://learn.microsoft.com/en-us/iis/extensions/planning-for-arr/application-request-routing-version-2-overview)
