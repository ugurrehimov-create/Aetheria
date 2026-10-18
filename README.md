# VesperNode v27 — Equipment-Aware Framing

This version builds on v21's Session Log improvements and improves how the saved imaging setup informs framing and exposure guidance.

## Equipment-aware framing
- Uses focal length and sensor width/height to calculate the actual angular field of view, plus focal ratio and image scale when the relevant values are supplied.
- The target details view uses SIMBAD's catalogued major axis, minor axis, and position angle (when available) to estimate the target's projected size at the selected camera rotation.
- Framing advice checks both frame dimensions and uses a 10% margin when the catalogued position angle is available. When it is not available, it reports a conservative major-axis check instead of pretending to know the orientation.
- Changing camera rotation updates the framing estimate, and the FOV overlay uses that rotation. The overlay requires focal length and both sensor dimensions.
- The text notes that catalogue sizes can omit faint outer structures; the fit estimate is a planning aid, not a guarantee of the final image composition.

## Mount-aware exposure advice
- Tripod-only setups can receive a rough NPF-rule untracked exposure estimate when focal length, aperture, and pixel size are provided.
- Star trackers and equatorial mounts are treated as tracking setups; actual limits still depend on alignment, guiding, and mount performance.
- Alt-azimuth mounts are treated as tracking-capable, but the app explicitly warns that field rotation may limit longer exposures.

## Session Log (from v21)
- Search, edit, and delete saved sessions.
- Record seeing, transparency, cloud cover, and guiding RMS.
- Export CSV and JSON backups; import JSON backups with record validation and ID-based merging.

## Data and offline note
Settings, marks, and sessions remain in browser local storage on that device. JSON export/import is a manual backup, not cloud sync. The service worker is available only when served from a supported HTTP/HTTPS origin. External sky/catalogue services are not made fully offline by this version.

## Validation performed
- JavaScript syntax check (`node --check` on extracted inline script).
- Duplicate HTML ID check.
- ZIP archive integrity test.
- Static checks for mount-aware guidance, camera-rotation refresh, and SIMBAD size/position-angle fields.

No claim is made that every browser interaction was tested live in this environment.


## v25 — Imaging control foundation
- Added Observe workspace for real Alpaca mount/camera/focuser/filter-wheel/rotator control when assigned and available.
- Added persistent local capture-sequence builder and camera exposure execution.
- Added explicit device capability/status messaging; no simulated hardware is shown as connected.
- Redesigned Tonight's imaging session marked-target cards so content uses the full card width instead of inheriting the generic event two-column layout.
- Fixed Marks panel action layout so Details and Go to belong to each mark instead of appearing as detached controls.
- Camera rotation state remains persisted per target.
- Service worker cache bumped to v25.

Validation note: source-level checks cover syntax, duplicate IDs and archive integrity. Real camera/focuser/filter/rotator hardware testing is not claimed without compatible Alpaca devices.


## v26 — Bug fixes, Planning/Log workflow, and capture foundations
- Moved Tonight's Imaging Session into Session Log so marked targets and planned events are together with one-click Log session actions.
- Planning events added to the plan now appear in the Log as separate planned items, with Log session and Remove actions.
- Fixed the Mark → imaging workflow persistence bug and kept target camera rotation persisted per mark ID/coordinates.
- Clicking empty map space now closes an open mark popup; mark hit tolerance was increased for easier selection.
- Deleting a marked target now clears its FOV overlay and closes stale target state.
- Bottom-bar controls are centered; sidebar controls are slightly larger; Observe uses a matching line icon.
- Map bottom-bar control now returns to the map/Home workspace instead of silently cycling survey names.
- Observe mount Abort Slew now checks whether the mount is actually slewing before sending the command.
- Added optional guide-camera assignment and a guiding-status foundation; AstraLog explicitly reports that Alpaca camera data alone does not provide guiding RMS.
- Added persistent last-capture summary after a completed capture sequence and a one-click Log capture action.
- Capture summary carries target, frame count, integration time, completion time, and active optical train into Session Log.
- Service worker cache bumped to v26.

Validation: JavaScript syntax check, duplicate HTML ID check, required-handler/static-reference checks, and ZIP integrity. Live hardware/browser interaction is not claimed without a compatible Alpaca setup.

## v27 — Map Surveys, Community Layout, and Gallery Foundation
- Map bottom-bar control now opens an explicit sky-survey chooser instead of cycling surveys invisibly.
- Added DSS2 color/red/blue, Pan-STARRS color, 2MASS, and AllWISE survey choices using Aladin Lite survey IDs.
- Explore and Connect hide the bottom bar and use the full available vertical workspace.
- Sidebar active-state highlighting now applies to working Settings, Gallery, Marks, HZ Calculator, and About windows.
- Replaced the Observe bottom-bar icon with Lucide Focus for consistency with the existing icon family.
- Added local Gallery with photo import, metadata, tags, processing/capture notes, favorites, delete/edit, local JSON export, and Post to Explore.
- Published Gallery items are shown in the local Explore workspace; real cross-user publishing still requires the future backend/account service.
- Images are resized/compressed for browser storage. This is a local gallery, not cloud backup.
- Validation: source JavaScript syntax, duplicate IDs, and ZIP integrity checked; no live browser/hardware test claimed.
