---
ref: network
lang: en
layout: page
title: "Academic Network"
nav_title: "Network"
nav_order: 8
permalink: /en/network/
redirect_from:
  - /network/
active_nav: network
---

{% assign current_lang = page.lang | default: "en" %}
{% assign locale = site.data.locales[current_lang] %}
{% assign network_api = site.analytics.endpoint | default: 'https://academy.banabirsebepver.com' | append: '/api/network.php' %}

<div class="fac-page network-page" data-endpoint="{{ network_api }}" data-lang="{{ current_lang }}">
  <div class="archive-page-container">
    <div class="container-fluid">

      <!-- Header Section -->
      <div class="archive-header network-header text-center">
        <h1><i class="fa fa-network-wired"></i> {{ locale.ui.network_title }}</h1>
        <p class="lead">
          {{ locale.ui.network_subtitle }}
        </p>
      </div>

      {% assign version = site.data.version %}
      {% assign local_tag = version.tag | default: "v0.1.1" %}
      {% assign local_date = version.build_date | default: "" %}

      <!-- Top Row: Call To Action (10/12) on Left & Version Status (2/12) on Right -->
      <div class="network-top-row">
        <!-- Call To Action Card (10/12) -->
        <div class="network-card network-cta-card">
          <div class="network-cta-content">
            <h3 class="network-cta-title">
              <i class="fa fa-code-fork"></i> {{ locale.ui.join_network_title | default: locale.ui.network_cta_title }}
            </h3>
            <p class="network-cta-desc">
              {{ locale.ui.join_network_desc | default: locale.ui.network_cta_desc }}
            </p>
          </div>
          <div class="network-cta-action">
            <a href="https://github.com/BanaBirSebepVer/Academy" target="_blank" rel="noopener noreferrer" class="btn btn-success network-cta-btn">
              <i class="fa fa-github"></i> {{ locale.ui.submit_site_button | default: locale.ui.network_cta_btn }}
            </a>
          </div>
        </div>

        <!-- Version Information Card (2/12) -->
        <div class="network-card version-card version-status-ok"
             id="versionStatusCard"
             data-local-version="{{ local_tag }}"
             data-local-date="{{ local_date }}"
             data-upstream-url="https://raw.githubusercontent.com/BanaBirSebepVer/Academy/main/_data/version.yml"
             data-lang="{{ current_lang }}">
          <div class="version-header">
            <h4 class="version-title">
              <i class="fa fa-code-fork"></i> {{ locale.ui.version_title | default: "Engine Version" }}
            </h4>
            <span class="version-status-pill" id="versionStatusPill">
              Up to date
            </span>
          </div>
          <div class="version-meta">
            <div class="version-meta-row">
              <span class="version-meta-label">{{ locale.ui.version_release | default: "Release" }}:</span>
              <span class="version-badge-val" id="versionBadgeVal">{{ local_tag }}</span>
            </div>
            <div class="version-meta-row">
              <span class="version-meta-label">{{ locale.ui.version_built | default: "Built" }}:</span>
              <span class="version-date-val" id="versionDateVal" title="{{ local_date }}">{{ local_date | default: "-" }}</span>
            </div>
          </div>
          <div class="version-status-text" id="versionStatusText">
            <i class="fa fa-check-circle"></i> <span>Up to date</span>
          </div>
        </div>
      </div>

      <!-- Filter & Search Controls Card -->
      <div class="network-controls-card">
        <!-- Live Search Input -->
        <div class="network-search-wrap">
          <div class="input-group">
            <span class="input-group-addon">
              <i class="fa fa-search"></i>
            </span>
            <input type="text" id="networkSearchInput" class="form-control network-search-input" placeholder="{{ locale.ui.search_network_placeholder | default: 'Search by name, university, field, or keywords...' }}">
          </div>
        </div>

        <!-- 4-Column Dropdown Select Filters -->
        <div class="row network-dropdowns-row">
          <!-- 1. Country Filter -->
          <div class="col-md-3 col-sm-6 col-xs-12 network-dropdown-col">
            <label for="networkFilterCountry" class="network-filter-label">
              <i class="fa fa-globe"></i> {{ locale.ui.filter_by_country | default: 'Country' }}
            </label>
            <select id="networkFilterCountry" class="form-control network-filter-select">
              <option value="all">{{ locale.ui.all_countries | default: 'All Countries' }}</option>
            </select>
          </div>

          <!-- 2. University / Institution Filter -->
          <div class="col-md-3 col-sm-6 col-xs-12 network-dropdown-col">
            <label for="networkFilterInstitution" class="network-filter-label">
              <i class="fa fa-university"></i> {{ locale.ui.filter_by_university | default: 'University' }}
            </label>
            <select id="networkFilterInstitution" class="form-control network-filter-select">
              <option value="all">{{ locale.ui.all_universities | default: 'All Universities' }}</option>
            </select>
          </div>

          <!-- 3. Academic Field Filter -->
          <div class="col-md-3 col-sm-6 col-xs-12 network-dropdown-col">
            <label for="networkFilterField" class="network-filter-label">
              <i class="fa fa-graduation-cap"></i> {{ locale.ui.filter_by_field | default: 'Field' }}
            </label>
            <select id="networkFilterField" class="form-control network-filter-select">
              <option value="all">{{ locale.ui.all_fields | default: 'All Fields' }}</option>
            </select>
          </div>

          <!-- 4. Keywords Filter -->
          <div class="col-md-3 col-sm-6 col-xs-12 network-dropdown-col">
            <label for="networkFilterKeyword" class="network-filter-label">
              <i class="fa fa-tags"></i> {{ locale.ui.filter_by_keyword | default: 'Keyword' }}
            </label>
            <select id="networkFilterKeyword" class="form-control network-filter-select">
              <option value="all">{{ locale.ui.all_keywords | default: 'All Keywords' }}</option>
            </select>
          </div>
        </div>

        <!-- Meta Bar: Live Counter & Reset Button -->
        <div class="network-meta-bar">
          <div class="network-counter-wrap">
            <span class="network-counter-badge">
              <span id="networkCurrentCount">0</span> / <span id="networkTotalCount">0</span>
            </span>
            <span>{{ locale.ui.members_count_suffix | default: 'members shown' }}</span>
          </div>

          <button id="networkResetFilters" class="btn btn-default network-reset-btn" type="button">
            <i class="fa fa-refresh"></i> {{ locale.ui.reset_filters | default: 'Reset' }}
          </button>
        </div>
      </div>

      <!-- No Results State -->
      <div id="networkNoResults" class="network-no-results" style="display: none;">
        <div class="network-no-results-panel">
          <i class="fa fa-search-minus icon-empty"></i>
          <h4>{{ locale.ui.no_network_found | default: 'No matching institutions or researchers found.' }}</h4>
          <p>{{ locale.ui.no_network_found_sub | default: 'Please try a different search term or clear active filters.' }}</p>
          <button class="btn btn-primary btn-sm network-reset-btn" type="button">
            <i class="fa fa-refresh"></i> {{ locale.ui.clear_filters | default: 'Clear Filters' }}
          </button>
        </div>
      </div>

      <!-- Network Cards Grid (Dynamically Populated from Database API) -->
      <div class="row network-grid" id="networkGrid">
        <div id="networkLoading" class="network-loading-state text-center" style="padding: 50px 15px; width: 100%;">
          <i class="fa fa-spinner fa-spin fa-2x" style="color: #2563eb; margin-bottom: 12px; display: inline-block;"></i>
          <p class="text-muted" style="margin-bottom: 0;">Loading academic network members...</p>
        </div>
      </div>

    </div>
  </div>
</div>

<script>
(function() {
  function checkEngineVersion() {
    var card = document.getElementById('versionStatusCard');
    if (!card || card.getAttribute('data-version-checked') === 'true') return;
    card.setAttribute('data-version-checked', 'true');

    var localVer = card.getAttribute('data-local-version') || 'v0.1.1';
    var localDateStr = card.getAttribute('data-local-date') || '';
    var upstreamUrl = card.getAttribute('data-upstream-url') || 'https://raw.githubusercontent.com/BanaBirSebepVer/Academy/main/_data/version.yml';
    var lang = card.getAttribute('data-lang') || 'en';

    var pill = document.getElementById('versionStatusPill');
    var statusText = document.getElementById('versionStatusText');

    function parseYaml(str) {
      var res = {};
      var lines = str.split('\n');
      for (var i = 0; i < lines.length; i++) {
        var m = lines[i].match(/^\s*([a-zA-Z0-9_-]+)\s*:\s*["']?(.*?)["']?\s*$/);
        if (m) res[m[1]] = m[2].trim();
      }
      return res;
    }

    function parseSemVer(v) {
      return (v || '').replace(/^v/i, '').split('.').map(function(n) { return parseInt(n, 10) || 0; });
    }

    function compareSemVer(v1, v2) {
      var p1 = parseSemVer(v1);
      var p2 = parseSemVer(v2);
      var len = Math.max(p1.length, p2.length);
      for (var i = 0; i < len; i++) {
        var n1 = p1[i] || 0;
        var n2 = p2[i] || 0;
        if (n1 > n2) return 1;
        if (n1 < n2) return -1;
      }
      return 0;
    }

    function parseDateMs(d) {
      if (!d) return 0;
      var ms = Date.parse(d);
      if (!isNaN(ms)) return ms;
      var m = d.match(/(\d{4})-(\d{2})-(\d{2})/);
      if (m) return new Date(m[1], m[2] - 1, m[3]).getTime();
      return 0;
    }

    function setStatus(type, pillLabel, textHtml) {
      card.classList.remove('version-status-ok', 'version-status-warn', 'version-status-danger');
      card.classList.add('version-status-' + type);
      if (pill) pill.textContent = pillLabel;
      if (statusText) statusText.innerHTML = textHtml;
    }

    fetch(upstreamUrl, { cache: 'no-cache' })
      .then(function(res) {
        if (!res.ok) throw new Error('HTTP ' + res.status);
        return res.text();
      })
      .then(function(yamlText) {
        var upstream = parseYaml(yamlText);
        var upstreamVer = upstream.tag || upstream.version || '';
        var upstreamDateStr = upstream.build_date || '';

        if (!upstreamVer && !upstreamDateStr) return;

        var vDiff = compareSemVer(upstreamVer, localVer);
        var localDate = parseDateMs(localDateStr);
        var upstreamDate = parseDateMs(upstreamDateStr);

        var repoUrl = 'https://github.com/BanaBirSebepVer/Academy';

        if (vDiff > 0) {
          var pUp = parseSemVer(upstreamVer);
          var pLoc = parseSemVer(localVer);
          if ((pUp[0] || 0) > (pLoc[0] || 0)) {
            setStatus('danger', 'Critical', '<i class="fa fa-exclamation-circle"></i> <a href="' + repoUrl + '/releases" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline;">Critical: ' + upstreamVer + '</a>');
          } else {
            setStatus('warn', 'Update', '<i class="fa fa-arrow-circle-up"></i> <a href="' + repoUrl + '/releases" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline;">New release: ' + upstreamVer + '</a>');
          }
        } else if (vDiff === 0 && upstreamDate > (localDate + (3600 * 1000))) {
          setStatus('warn', 'Update', '<i class="fa fa-arrow-circle-up"></i> <a href="' + repoUrl + '" target="_blank" rel="noopener noreferrer" style="color: inherit; text-decoration: underline;">New patch available</a>');
        } else {
          setStatus('ok', 'Up to date', '<i class="fa fa-check-circle"></i> <span>Up to date</span>');
        }
      })
      .catch(function(err) {
        console.warn('[Academy Version] Could not check upstream version.yml:', err);
      });
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', checkEngineVersion);
  } else {
    checkEngineVersion();
  }
})();
</script>
