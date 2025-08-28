---
layout: page
title:
permalink: /projects/
comment: false
latex: true
---
* TOC
{:toc}

<div class="contact">
{% if site.github_username %}
        <a href="https://github.com/{{ site.github_username }}">GitHub</a>
{% endif %}
{% if site.twitter_username %}
        <a href="https://twitter.com/{{ site.twitter_username }}">Twitter</a>
{% endif %}
{% if site.email %}
        <a href="mailto:{{ site.email }}">Email</a>
{% endif %}
        <a href="{{ "/feed.xml" | prepend: site.baseurl }}">RSS</a>
</div>

<main class="p-6">
  <!-- Summary Section -->
  <section class="max-w-prose mx-auto prose p-6">
    <h1>Projects</h1>
    <p>A running list of projects I've built.</p>
    <p><span class="font-bold">Total Projects:</span> 5</p>
    <ul>
      <li>🟢 <span class="font-bold">Active:</span> 2 - Currently developing</li>
      <li>🟡 <span class="font-bold">Passive:</span> 2 - Running but not developing</li>
      <li>🔴 <span class="font-bold">ShutDown:</span> 1 - No longer running</li>
    </ul>
  </section>

  <!-- Active -->
  <section class="max-w-3xl mx-auto prose">
    <h2>Active Projects</h2>
    <table>
      <thead class="font-semibold border-b">
        <tr>
          <th>State</th>
          <th>Name</th>
          <th>Start</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>🟢</td>
          <td class="px-2">Relative Strength Screener</td>
          <td>2023</td>
          <td>KOSPI/KOSDAQ/NASDAQ relative strength rotation tool</td>
        </tr>
        <tr>
          <td>🟢</td>
          <td class="px-2">Short Momentum Nasdaq Screener</td>
          <td>2024</td>
          <td>Momentum strategy applied to Nasdaq shorts</td>
        </tr>
      </tbody>
    </table>
  </section>

  <!-- Passive -->
  <section class="max-w-3xl mx-auto prose p-6">
    <h2>Passive Projects</h2>
    <table>
      <thead class="font-semibold border-b">
        <tr>
          <th>State</th>
          <th>Name</th>
          <th>Start</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>🟡</td>
          <td class="px-2">Spitfire Systematic Trading</td>
          <td>2025</td>
          <td>Framework for systematic trading strategies</td>
        </tr>
        <tr>
          <td>🟡</td>
          <td class="px-2">TradeScope Dashboard</td>
          <td>2025</td>
          <td>Trading asset management dashboard</td>
        </tr>
      </tbody>
    </table>
  </section>

  <!-- Shutdown -->
  <section class="max-w-3xl mx-auto prose p-6">
    <h2>Shutdown Projects</h2>
    <table>
      <thead class="font-semibold border-b">
        <tr>
          <th>State</th>
          <th>Name</th>
          <th>Start</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>🔴</td>
          <td class="px-2">Bitcoin Whale Transaction Detect</td>
          <td>2022</td>
          <td>Tracked on-chain whale transactions for signal generation</td>
        </tr>
      </tbody>
    </table>
  </section>

  <!-- All Projects -->
  <section class="max-w-3xl mx-auto prose p-6">
    <h2>All Projects</h2>
    <p>Complete list of projects including active, passive, and shutdown.</p>
    <table>
      <thead class="font-semibold border-b">
        <tr>
          <th>State</th>
          <th>Name</th>
          <th>Start</th>
          <th>Category</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>🟢</td>
          <td class="px-2">Relative Strength Screener</td>
          <td>2023</td>
          <td>Active</td>
          <td>KOSPI/KOSDAQ/NASDAQ relative strength rotation tool</td>
        </tr>
        <tr>
          <td>🟢</td>
          <td class="px-2">Short Momentum Nasdaq Screener</td>
          <td>2024</td>
          <td>Active</td>
          <td>Momentum strategy applied to Nasdaq shorts</td>
        </tr>
        <tr>
          <td>🟡</td>
          <td class="px-2">Spitfire Systematic Trading</td>
          <td>2025</td>
          <td>Passive</td>
          <td>Framework for systematic trading strategies</td>
        </tr>
        <tr>
          <td>🟡</td>
          <td class="px-2">TradeScope Dashboard</td>
          <td>2025</td>
          <td>Passive</td>
          <td>Trading asset management dashboard</td>
        </tr>
        <tr>
          <td>🔴</td>
          <td class="px-2">Bitcoin Whale Transaction Detect</td>
          <td>2022</td>
          <td>Shutdown</td>
          <td>Tracked on-chain whale transactions for signal generation</td>
        </tr>
      </tbody>
    </table>
  </section>
</main>