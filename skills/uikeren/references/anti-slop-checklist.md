# Anti-AI-Slop Checklist

Reject and replace any of the following cliché patterns before shipping:

## Layout & Visual Slop
- [ ] **No generic neon purple/indigo gradient blobs** over dark/white generic
      SaaS backgrounds unless the brand genuinely calls for it.
- [ ] **No cookie-cutter 3-column symmetric feature cards** with identical
      round colored icon circles + 1 heading + 2 lines of filler text.
- [ ] **No hollow hero template** ("big centered headline + 2 pill buttons +
      floating mockup box") without strong typographic rhythm or visual motif.
- [ ] **No repetitive Tailwind `rounded-2xl shadow-lg p-6` everywhere**—vary
      surface framing, borders, spacing, and visual hierarchy.

## Copy & Content Slop
- [ ] **No cliché AI buzzwords**: Ban *"Revolutionize"*, *"Seamless"*,
      *"Unleash"*, *"Next-gen"*, *"Elevate your journey"*, or stiff machine
      translations in Indonesian like *"Tingkatkan pengalaman Anda secara mulus"*.
- [ ] **No Lorem Ipsum or empty placeholders**: Use concrete, domain-authentic
      items, numbers, prices, schedules, or stories.

## Interaction Slop
- [ ] **No dead buttons or fake links**: Every CTA, nav item, tab, card, or
      filter must either navigate meaningfully, open a working modal/drawer, or
      update live UI state.
- [ ] **No static "fake app"**: Include real stateful JS interaction (e.g.,
      switcher, calculator, builder, cart, search/filter, or interactive preview).
- [ ] **No jarring or sluggish animations**: Animate GPU-friendly properties
      (`transform`, `opacity`), add `prefers-reduced-motion` support, and avoid
      layout-thrashing scroll handlers.
