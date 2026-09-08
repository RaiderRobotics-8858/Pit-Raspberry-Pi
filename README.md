# FRC MatchMaker

FRC MatchMaker is an independently developed video processing and publishing system for FIRST Robotics Competition events.

Its purpose is to turn long-form event video into individual match videos, associate those videos with the correct competition data, produce consistent match graphics, and publish the finished matches to YouTube in a way that is easy for teams and event participants to navigate for scouting.

The project is designed around a simple idea:

> A robotics team should not have to search through hours of livestream footage to find its matches.

FRC MatchMaker automates that work.

---

## What FRC MatchMaker Does

FRC MatchMaker processes event video and competition data to create individual match deliverables.

For each match, the system can:

* Identify and isolate the relevant section of event video
* Associate the video with the correct FRC match
* Generate match-specific title and score graphics
* Validate the resulting match deliverable
* Preserve replay and repair information
* Publish the completed video to YouTube
* Apply match-specific metadata and thumbnails
* Add the video to an event playlist
* Add the video to team-specific playlists for all six participating teams

The result is a searchable and organized video library rather than a collection of multi-hour event broadcasts.

---

## Why It Exists

FIRST Robotics Competition events generate a large amount of valuable video.

That footage can be useful for:

* Team scouting
* Match review
* Driver and strategy analysis
* Mentor and student review
* Event documentation
* Sharing matches with families and supporters
* Post-event analysis
* Preserving competition history

The problem is that event video is commonly published as long livestream recordings or large VOD files.

Finding one match may require manually locating the correct broadcast, identifying the approximate timestamp, and scrubbing through the recording.

FRC MatchMaker is intended to remove that friction.

A team-specific playlist can provide direct access to that team's entire event without requiring the viewer to search through the original broadcast.

---

## System Overview

FRC MatchMaker is built as a set of cooperating components rather than a single monolithic process.

The system currently includes functionality for:

### Event Data

Competition information is associated with event and match records so video segments can be matched with the correct teams, scores, rankings, and match identifiers.

The Blue Alliance is used as a source of publicly available FRC event information.

### Media Intake

FRC MatchMaker can work with both live event media and completed VOD sources.

Live event operation is designed around a growing local media buffer so matches can be processed while the event is still in progress.

Completed event video can also be processed after the event.

### Match Detection and Segmentation

The system identifies match boundaries within the event video and creates persistent match segment records.

Segments retain source information so media from different livestreams, event days, or finalized VOD files can be handled without assuming they share the same timeline.

### Match Binding

Detected video segments are associated with FRC match records.

The system is designed to handle real event conditions such as:

* Replayed matches
* Missing or incomplete detections
* Back-to-back occurrences of the same match
* Multiple event-day video sources
* Manual repair of unidentified segments

### Graphics and Deliverables

FRC MatchMaker generates match-specific visual assets and final video deliverables.

These may include:

* Match title graphics
* Score graphics
* Team information
* Ranking information
* Match metadata
* Replay-specific output

The original event video remains separate from the final published deliverables.

### Quality Control and Manual Repair

Automation is intended to do most of the work, but real event video is imperfect.

FRC MatchMaker includes operator-assisted review and repair workflows for cases where automatic processing cannot confidently determine the correct result.

This allows individual problems to be corrected without restarting or rebuilding the entire event.

### YouTube Publishing

Finished and certified match videos can be published through the YouTube Data API.

The publisher manages:

* Video uploads
* Titles and descriptions
* Tags
* Custom thumbnails
* Processing status
* Visibility
* Event playlists
* Team playlists
* Recovery from partial publishing operations

Each normal match is intended to appear in:

* One event playlist
* Six team playlists

This playlist structure is a core part of the product.

For example, a team can open its event playlist and immediately see every match in which it participated.

---

## Live Event Operation

FRC MatchMaker is being developed with live-event use as a primary goal.

The intended workflow is:

```text
Live Event Video
        ↓
Local Media Buffer
        ↓
Match Detection
        ↓
Match Identification
        ↓
Graphics / Processing
        ↓
Quality Control
        ↓
Certified Match Video
        ↓
YouTube Publishing
        ↓
Event + Team Playlists
```

The objective is to make completed matches available while the tournament is still underway rather than waiting until the event is over.

The system is also designed to resume after interruption and preserve completed work rather than treating every restart as a new event.

---

## Publishing Philosophy

FRC MatchMaker treats publishing as a recoverable workflow.

A successful upload is recorded immediately so later API failures do not create duplicate videos.

Subsequent publishing steps can be repaired independently, including:

* Playlist membership
* Metadata
* Thumbnail assignment
* Processing verification
* Visibility changes

A video does not need to be re-uploaded simply because a later publishing operation failed.

Custom thumbnails are treated as best-effort and do not prevent an otherwise completed match from being made public.

Event organization and playlist membership remain a major part of the publishing workflow.

---

## Event and Team Playlists

Playlist organization is one of the primary features of FRC MatchMaker.

An event playlist provides chronological access to the event's individual match videos.

Team playlists provide a filtered view of that same event.

A match with six participating teams is normally added to seven playlists:

```text
1 Event Playlist
6 Team Playlists
----------------
7 Playlist Memberships
```

This allows the published video collection to function as an event archive, a scouting resource, and a team-specific match library at the same time.

---

## Replays and Corrections

FRC events occasionally replay matches.

FRC MatchMaker is designed to preserve replay occurrences rather than assuming that a match number corresponds to only one piece of video.

The system also supports repair workflows for:

* Missing matches
* Incorrect segment boundaries
* Incorrect match associations
* Source transitions
* Replayed matches
* Publishing failures

The long-term goal is for corrections to be targeted and recoverable without disrupting already completed matches.

---

## Hardware and Deployment

The current development platform is a Raspberry Pi-based event system with local external storage.

The system has been developed for operation in a tournament environment, including:

* Local event media storage
* HDMI operator/display output
* MPV-based video review
* Keyboard-driven repair controls
* Persistent event state
* Independent publishing tools

The architecture is intended to keep event processing local while using external services only where appropriate, such as competition data and YouTube publishing.

---

## Project Status

FRC MatchMaker is under active development.

Major capabilities already implemented or in active testing include:

* Event repository management
* Live and VOD media handling
* Match detection and segmentation
* Match-to-video association
* Replay-aware processing
* Manual repair workflows
* Match title and score graphics
* Certified match deliverables
* YouTube publishing
* Event playlists
* Team playlists
* Persistent publishing state
* Recovery from partial API failures
* Live-event additional statistics display concepts

Development continues around scalability, publishing limits, event presentation, replay handling, and broader live-event deployment.

---

## YouTube API Usage

FRC MatchMaker uses YouTube API Services to manage its publishing workflow.

API operations may include:

* Uploading match videos
* Updating video metadata
* Updating video visibility
* Uploading custom thumbnails
* Creating playlists
* Adding videos to playlists
* Reading processing status
* Reading basic authenticated channel information

FRC MatchMaker uses Google OAuth 2.0 authorization for operations performed on the authorized YouTube account.

The publisher is currently an operator-run application and is not a public bulk-upload service.

---

## Data Sources

FRC MatchMaker may use publicly available FRC competition information from services including The Blue Alliance.

The Blue Alliance is an independent third-party service.

FRC MatchMaker is not affiliated with or operated by The Blue Alliance.

---

## Independence and Trademarks

FRC MatchMaker is an independent project.

It is not affiliated with, sponsored by, endorsed by, or operated by:

* FIRST
* FIRST Robotics Competition
* Google
* YouTube
* The Blue Alliance
* Participating teams
* Event organizers
* Broadcasters
* Venues

All third-party names, trademarks, logos, video, competition data, and other materials remain the property of their respective owners.

---

## Privacy Policy

FRC MatchMaker's Privacy Policy is available here:

[[Privacy Policy](./PRIVACY.md)](https://github.com/RaiderRobotics-8858/Pit-Raspberry-Pi/blob/main/FRCMatchMakerPrivacyGoogle.md)

---

## Terms of Service

FRC MatchMaker's Terms of Service are available here:

[Terms of Service](./TERMS.md)

---

## Contact

Questions about FRC MatchMaker may be directed to:

**FRC MatchMaker**
**Email:** [fcrmatchmaker@gmail.com](mailto:fcrmatchmaker@gmail.com)
