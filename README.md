# A Stock Price Analyzer <a href="https://eloquent-panini-ff23b8.netlify.com/">Try Me!</a>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

![GitHub issues](https://img.shields.io/github/issues/harrymwinters/stock-price-delta)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-green.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Docker Automated build](https://img.shields.io/docker/automated/harrymwinters/stock-price-delta)
![Netlify Status](https://api.netlify.com/api/v1/badges/b6dd4174-209a-4dac-9494-cc122bb18daa/deploy-status)


## Table of Contents

- [Overview](#Overview)
- [Features](#Features)
- [Getting Started](<#Getting\ Started>)
- [Links](#Links)
- [Credits & Acknowledgments](<#Credits\ &\ Acknowledgments>)

## Overview

When an unnamed finiancial institution took 3 months to transfer some significant funds I began to wonder how much market growth (or loss) I was missing out on.

## Features

This app allows one to specify a publically traded stock (or stocks) by ticker symbol and view the change in it's value during any window in the last 19 years.

<div>
    <h1>
    Date range selector up to 19 years a ago.
    </h1>
    <img style="float: left;" 
        src="https://github.com/harrymwinters/stock-price-delta/blob/master/media/Date Select.png" 
        width=40%>
    <h1> 
    See the price trends over time 
    </h1>
    <img style="float: right;" 
        src="https://github.com/harrymwinters/stock-price-delta/blob/master/media/Main Screen.png" 
        width=80% >
    <h1> 
    And a summary of thier changes. 
    </h1>
    <img 
    src="https://github.com/harrymwinters/stock-price-delta/blob/master/media/Summary.png"  
        width=40% >
</div>

## Getting Started

If you're just interested in viewing the app running you can check it out [Here](https://--). If you want to run it locally, check out the make commands.

`make run_dev` is an alias for `npm run serve` and there's a similiar alias `make run_prod` to run the latest docker image locally.

Otherwise, standard vue and npm commands apply.

## Links

- [Icons](https://www.flaticon.com/)
- [LinkedIn](https://www.linkedin.com/in/code-bio/)
- [Hosted App](https://eloquent-panini-ff23b8.netlify.com/)

## Credits & Acknowledgments

<ul>
<li>Icons made by <a href="https://www.flaticon.com/authors/smashicons" title="Smashicons">Smashicons</a> from <a href="https://www.flaticon.com/"         title="Flaticon">www.flaticon.com</a></li>

<li>Icons made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/"             title="Flaticon">www.flaticon.com</a></li>

<li>Stock info provided by <a href="https://www.alphavantage.co"> Alpha Vantage </a></li>

<li> I used <a href="https://www.echartsjs.com/en/index.html"> echarts </a> for plotting.</li>

<li>I used <a href="https://www.favicon.cc/"> echarts </a> for favicon generation.</li>
</ul>
