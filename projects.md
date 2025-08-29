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
  <a href="{{ "/feed.xml" | relative_url }}">RSS</a>
</div>

<!-- 여기에 JS가 내용을 주입할 타겟 -->
<div id="projects-app"></div>

<script>
const projects = [
  { state: "🟢", status: "Active", name: "Relative Strength Screener", start: 2023, desc: "KOSPI/KOSDAQ/NASDAQ relative strength scores" },
  { state: "🟢", status: "Active", name: "Short Momentum Nasdaq Screener", start: 2024, desc: "Momentum strategy applied to Nasdaq shorts" },
  { state: "🟡", status: "Passive", name: "Spitfire Systematic Trading", start: 2025, desc: "live execution of systematic trading strategies in BTC/ETH market" },
  { state: "🟡", status: "Passive", name: "Trading asset management dashboard", start: 2025, desc: "dashboard for performance analytics: win rate, risk-reward ratio, trade frequency, and rule adherence tracking" },
  { state: "🔴", status: "Shutdown", name: "Bitcoin Whale Transaction Detect", start: 2022, desc: "Tracked on-chain whale transactions for signal generation" }
];

function renderSummary(list) {
  const total = list.length;
  const active = list.filter(p => p.status === "Active").length;
  const passive = list.filter(p => p.status === "Passive").length;
  const shutdown = list.filter(p => p.status === "Shutdown").length;
  return `
    <section class="max-w-prose mx-auto prose p-6">
      <h1>Projects</h1>
      <p>A running list of projects I've built.</p>
      <p><span class="font-bold">Total Projects:</span> ${total}</p>
      <ul>
        <li>🟢 <b>Active:</b> ${active}</li>
        <li>🟡 <b>Passive:</b> ${passive}</li>
        <li>🔴 <b>Shutdown:</b> ${shutdown}</li>
      </ul>
    </section>
  `;
}

function renderTable(title, list) {
  if (!list.length) return "";
  return `
    <section class="max-w-3xl mx-auto prose p-6">
      <h2>${title}</h2>
      <table>
        <thead>
          <tr><th>State</th><th>Name</th><th>Start</th><th>Description</th></tr>
        </thead>
        <tbody>
          ${list.map(p => `
            <tr>
              <td>${p.state}</td>
              <td class="px-2">${p.name}</td>
              <td>${p.start}</td>
              <td>${p.desc}</td>
            </tr>
          `).join("")}
        </tbody>
      </table>
    </section>
  `;
}

document.getElementById("projects-app").innerHTML = `
  ${renderSummary(projects)}
  ${renderTable("All Projects", projects)}
  ${renderTable("Active Projects", projects.filter(p => p.status === "Active"))}
  ${renderTable("Passive Projects", projects.filter(p => p.status === "Passive"))}
  ${renderTable("Shutdown Projects", projects.filter(p => p.status === "Shutdown"))}
`;
</script>
