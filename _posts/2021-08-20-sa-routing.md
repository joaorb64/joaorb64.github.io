---
layout: post
published: true
title: "On South America's internet routing"
date: 2021-08-20
comments: true
categories:
---

{% assign image_path = page.slug | prepend: '/img/post_images/' %}

## On South America's internet routing

In this brief post, I will go over data I have gathered on South America's routing. The idea was to test connections between different countries in SA to try to find some kind of pattern. I have created a test using the database from here: [https://williamyaps.github.io/wlmjavascript/servercli.html](https://williamyaps.github.io/wlmjavascript/servercli.html). I have created a script that tries PINGing all servers from a few cities in SA and record the results. I have sent this script to some players from different regions and gathered the results.

I have also generated maps showing the gathered data, which you can see below. Values with (+) mean they were the best connections, while values with (-) mean they were the worst connections. In general, consider something close to (+) as the actual value.

You can also find the raw values and the images here: [RAW values](https://github.com/joaorb64/joaorb64.github.io/tree/master/img/post_images/sa-routing/data).

Notice that the same company (Telefónica) owns Vivo and Movistar, which probably explains why their connection is so good: they are available in most countries in South America. So it makes sense that this company owns access to multiple different routes.

# ARGENTINA

## MOVISTAR

![]({{image_path}}/data/plot_ar_movistar.png)

# BRAZIL

## Rio de Janeiro - Vivo

![]({{image_path}}/data/plot_br_rj_vivo.png)

## Santa Catarina - NET/Claro

Terrible routing.

![]({{image_path}}/data/plot_br_sc_net.png)

## Santa Catarina - Vivo

![]({{image_path}}/data/plot_br_sc_vivo.png)

## São Paulo - Vivo

![]({{image_path}}/data/plot_br_sp_vivo.png)

# CHILE

## Movistar

![]({{image_path}}/data/plot_cl_movistar.png)

## Claro

![]({{image_path}}/data/plot_cl_claro.png)

## VTR

![]({{image_path}}/data/plot_cl_vtr.png)

## Mundo Pacifico

![]({{image_path}}/data/plot_cl_mundopacifico.png)

## Unknown ISP

![]({{image_path}}/data/plot_cl_unk.png)
![]({{image_path}}/data/plot_cl_unk2.png)

# COLOMBIA

Bad routing to the rest of South America.

## Claro

![]({{image_path}}/data/plot_co_claro.png)

## Unknown ISP

![]({{image_path}}/data/plot_co_unk.png)

# ECUADOR

Bad routing to the rest of South America.

## Netlife

![]({{image_path}}/data/plot_ec_netlife.png)
![]({{image_path}}/data/plot_ec2_netlife.png)
![]({{image_path}}/data/plot_ec3_netlife.png)

# PERU

## Movistar

![]({{image_path}}/data/plot_pe_movistar.png)

## WIN

![]({{image_path}}/data/plot_pe_win.png)

In general, what can be concluded from this data:

- **There is a connection gap between [ Ecuador, Colombia, Venezuela ], and the rest of SA.** Just like every other country has ~40-50ms ping with nearby countries, those countries have this delay when connecting to Central and North America. I've heard Ecuador can get pings as low as 60ms to US's West Coast, which is incredibly good. One reason could be that the connection goes north to the USA before going back south to South America, adding extra delay. There are cables on the west coast of SA connecting Ecuador and Colombia directly to other countries, but it seems like none of the tested ISPs uses those routes. In conclusion: *when doing region locked online tournaments, optimally, those countries shouldn't be playing with South America but rather Central America instead*. 
- Some ISPs (such as Brazil's non-fiber Claro/NET) have terrible connection to the rest of South America because of routing issues. The signal goes north to Miami before going back south, adding unplayable amounts of delay.