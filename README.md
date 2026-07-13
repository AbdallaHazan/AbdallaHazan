name: Metrics
on:
  schedule:
    # Runs once a day at midnight UTC — adjust as you like
    - cron: "0 0 * * *"
  workflow_dispatch: {}
  push:
    branches:
      - main

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: ${{ secrets.METRICS_TOKEN }}
          user: AbdallaHazan
          filename: github-metrics.svg
          template: classic

          # --- Base sections ---
          base: header, activity, community, repositories

          # --- Isometric commit calendar ---
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year

          # --- Languages breakdown ---
          plugin_languages: yes
          plugin_languages_analysis_timezone: Africa/Mogadishu
          plugin_languages_categories: markup, programming
          plugin_languages_recent_categories: markup, programming
          plugin_languages_details: percentage

          # --- Achievements ---
          plugin_achievements: yes
          plugin_achievements_threshold: C

          # --- Lines of code changed ---
          plugin_lines: yes
