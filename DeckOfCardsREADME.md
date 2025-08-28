Deck of Cards API – QA Test Collection
1. Purpose of the Collection
The Postman collection was created to ensure structured and repeatable testing of the Deck of Cards API.
Key objectives:
Regression testing of all endpoints.
Exploratory testing of parameters and edge cases.
Automation of business scenarios (e.g., Blackjack).
Providing documentation and examples for QA and development teams.
2. Approach to Collection Design
The collection is organized into three layers:
A. Core API Functionality
Create new decks (with/without jokers, partial decks).
Shuffle existing decks.
Draw cards.
Manage piles (add, list, draw).
Return cards to the deck.
These requests cover the primary functionality described in the API documentation.
B. Blackjack Game Scenario
A dedicated set of requests was added to simulate a Blackjack game flow:
Confirm the API is available.
Create a new deck.
Shuffle the deck.
Deal three cards to each of two players.
Calculate card values (Ace=1 or 11, Face=10).
Check whether either player has Blackjack.
Report which player wins or whether there is a tie.
This demonstrates end-to-end usage of the API and validates business logic, not just endpoint responses.
C. Error and Edge Case Tests
Since the official documentation lacks detail on errors and limits, additional requests were created:
E1. Draw More Cards Than Available
 Requesting 60 cards from a 52-card deck returns fewer cards but still success=true.
 Documentation gap: behavior on overdraw not defined.
E2. Too Many Decks
 deck_count=9999 often succeeds. Maximum supported value is not defined.
E3. Invalid Parameters
 deck_count=abc produces unclear results. Documentation should describe expected error format.
E4. Negative or Zero Count
 draw/?count=-5 sometimes returns empty results silently instead of error.
E5. Unsupported Methods
 Sending PUT or DELETE to endpoints should return 405 Method Not Allowed, but this is not documented.
3. Proposed Documentation Improvements
The current API documentation is minimal. Improvements recommended:
Missing Endpoints
GET /api/deck/{deck_id} → fetch current deck status.
DELETE /api/deck/{deck_id} → remove a deck.
GET /api/deck/{deck_id}/piles → list all piles.
Clarify Behavior
Define maximum deck_count.
Define maximum draw count and handling of overdraws.
Explain rules for returning cards (are they auto-shuffled or appended?).
State explicitly that only GET is supported.
Error Handling
Provide error response examples (400, 404, 405).
Define consistent structure for error messages.
Usability
Add POST examples as an alternative to GET with query parameters.
Add JSON schemas for request and response bodies.
Provide best practices for using unique deck_id and avoiding caching.
4. Benefits
Comprehensive coverage of both functional and negative scenarios.
Increased confidence in API stability and correctness.
Clear feedback to API maintainers regarding missing documentation.
Collection can serve as living knowledge base for QA and development teams.
