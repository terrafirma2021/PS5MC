# Overdrive in PS5MC

PS5MC is the application. Kodi owns the window system, media playback, settings,
skins, and update path. Overdrive becomes a built-in PS5MC subsystem rather than
another executable or a Python add-on.

The integration has three native parts:

1. A catalog model reads versioned JSON and exposes titles, releases, and local
   install state. The importer accepts the recovered Overdrive catalog as input;
   catalog data is separate from Kodi's source and can be refreshed without
   rebasing Kodi.
2. A Kodi media window presents Browse, Homebrew, Downloads, and Library through
   Kodi's view and theme controls. The same controller, focus, search, and artwork
   behaviour applies to media and store screens.
3. A PS5 download and install service owns transfers, archive extraction,
   verification, and ShadowMount registration. It never blocks Kodi's UI thread.

The first code slice adds the native window and catalog browsing. Download and
install operations will only be exposed after the service has persistent jobs,
verified downloads, and a PS5 hardware test. This keeps the store visible while
avoiding controls that appear to install content but do nothing.

The recovered Overdrive sources are reference implementations for behaviour and
data format. PS5MC's existing Kodi/Kodi 22 code and PS5 platform code remain the
source of truth for rendering and playback.
