BusinessKnot is an application for many-to-many (initially 1-1) face-to-face business meetings
based on profile matches and location.

BusinessKnot inherits some of the functionality from FaceOP, which is at Beta stage and
available at Google Play.

BusinessKnot basic functionality explained as pseudocode:

==========================
variables & constants:
==========================

CURRENT_LOCATION // current geographical location of the user
MEETING_PLACE // all available (local or global) meeting places (e.g. cities)
MEETING_POINT // exact meeting point, e.g. a restaurant (name, lat, long)
ANCHOR // accepted meeting position in lat, long or e.g. city, town
ANCHOR_RADIUS // accepted distance radius from anchor as a meeting point
MEETING_TYPE = [LUNCH, FREE, WORK, INSTANT]
TRUST_VALUE_RATING // user's achieved trust value/rating
MIN_TRUST_VALUE // required minimum trust value for a meeting
MAX_RADIUS // user defined accepted max ANCHOR_RADIUS
ALLOW_CONTACTING // allow contacting depending on condition (requires match() )
CRITERIA_FOR_MATCHING // includes e.g. profession, motivation, goals, character, interests etc.
MATCH_DATA_SOURCE // includes e.g. LinkedIn, other some accounts,
                  // written profile, selections, common contacts/friends/interests etc.

AVAILABLE_FOR_INSTANT_MEETS // true, if I'm available for instant meets
==========================
pseudocode key functions:
==========================

// matching meetings for a local or global meeting place

 for each MEETING_PLACE
        results = match(profile); // match against other profiles
        for each result in results
           if (TRUST_VALUE_RATING > MIN_TRUST_VALUE)
              suggestAMeeting(USER, MEETING_POINT); // suggest a meeting with USER
              // at MEETING_POINT


match(profile); // match on similarity based on profile data

function match(profile) {
  if (AVAILABLE) // if matched user is available
     schedule_meeting();
}

function informMatchRate() {
    if (USER_DISTANCE < ANCHOR_RADIUS)
       printMatchRate(); // how well we could match?
        if match_rate > treshold_value then
          inform both parties(); // both parties have to agree on this at their profile!
}

// (auto)scheduling vs. suggestion is determined by the MEETING_TYPE
schedule_meeting() {
   reserve calendar();
   change availability();
}

if match THEN suggest a meeting OR contact
// if meeting is not currently possible, allow contacting if that allowance flag was set

while (meeting_is_active)
  block_other_meetings(); // in calendar or disable suggestions etc.

rate(MEETING_ID) { // possible to do after a meeting
  rateMeeting(MEETING_ID); // rate this very meeting
  for each participant of MEETING_ID
      give_a_rating(participant); // calculates then new TRUST_VALUE_RATING of the participant
}


==============================
Key profile data for matching
==============================

location:           if location_A = location_B
profession:         if profession_A = profession_B
meeting language:   if language_A = language_B
generally:          if criterion_A = criterion_B
availability:       if time_available_A = time_available_B
MEETING_TYPE:       [LUNCH, FREE, WORK, INSTANT,...] // user can define accepted meeting types
