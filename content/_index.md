---
title: 'Ectopass'
layout: hextra-home
params:
  width: wide
---

{{< hextra/hero-container image="static/spectre.png" >}}

<div class="hx:mt-6 hx:mb-6">
{{< hextra/hero-headline >}}
  Quickly find Spectre gadgets
{{< /hextra/hero-headline >}}
</div>

<div class="hx:mb-12">
{{< hextra/hero-subtitle >}}
  Ectopass scans your code and detects if it contains Spectre-V1 vulnerabilities.
{{< /hextra/hero-subtitle >}}
</div>

<div class="hx:mb-10">
{{< hextra/hero-button text="Get a license" link="pricing" >}}
{{< hextra/hero-button text="Documentation" link="docs" style="margin-left:10px; background-color: transparent; border: 2px solid white"  >}}
</div>

{{< /hextra/hero-container >}}

{{< hextra/feature-grid cols=3 >}}
  {{< hextra/feature-card
    icon="fast-forward"
    title="Fast"
    subtitle="Relies on  Control Flow Graphs to analyse large files quickly. Does not perform symbolic execution."
    style="background: radial-gradient(ellipse at 50% 80%,rgba(194,97,254,0.15),hsla(0,0%,100%,0));"
    >}}
  {{< hextra/feature-card
    icon="desktop-computer"
    title="Easy to use"
    subtitle="Strong defaults to find gadgets with no configurations."
    style="background: radial-gradient(ellipse at 50% 80%,rgba(142,53,74,0.15),hsla(0,0%,100%,0));"
    >}}
  {{< hextra/feature-card
    icon="sparkles"
    title="Configurable"
    subtitle="Get more precise results by adapting the analysis to your system."
    style="background: radial-gradient(ellipse at 50% 80%,rgba(221,210,59,0.15),hsla(0,0%,100%,0));"
    >}}
  {{< hextra/feature-card
    icon="eye-off"
    title="Language agnostic"
    subtitle="Work with all languages compilable to LLVM IR: C, C++, Rust, Swift, etc..."
    >}}
  {{< hextra/feature-card
    icon="collection"
    title="CI friendly"
    subtitle="Easily deploy on your CI server to detect Spectre gadgets before you merge."
    >}}
  {{< hextra/feature-card
    icon="document-text"
    title="Simple licensing model"
    subtitle="Unlimited use of the tool per project, per year.">}}
{{< /hextra/feature-grid >}}

{{< playground >}}
