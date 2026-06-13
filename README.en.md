# Extraction Shooter Map Design Whitepaper: PvPvE, POI, Extraction Pressure, Telemetry
> Language / 语言：[中文](README.md) | English
>
> An extraction map is more than a place to fight. Resource layout, enemy pressure, and extraction points keep pushing players to choose between risk and reward.
>
> This production-facing whitepaper puts topology, POI scripts, spawn and extraction design, PvPvE, anti-camping cost, and telemetry into one review framework. The original Border Industrial Quarantine Zone case is a method demo, not a validated production map.
>
> Author: 魔魔王; version: v1.0; publication date: 2026-06-13.
>

## The Short Version

- An extraction-shooter map cannot be reviewed only as an arena or a scenic space. It has to put loss, reward, time, and information into the same match so every move creates a cost or an opportunity.
- Topology, POI scripts, spawn points, extraction points, and PvE should not be reviewed separately. If one layer breaks, players explain reward and death differently.
- Ambush play can exist, but free camping should not. Good maps make ambushes spend time, information, ammo, or extraction-window value.
- Border Industrial Quarantine Zone is an original method case, not a validated production map; it needs graybox testing and telemetry calibration before production use.

## How To Read This Report

- Complete report: keep reading this page.
- Compact index: [INDEX.en.md](INDEX.en.md).
- Chinese edition: [README.md](README.md).
- Evidence boundary: the original case, image notes, and references are collected at the end.

Map, level, system, numerical and operational collaboration documents for R&D teams

Version: v1.0
Case Map: Border Industrial Quarantine Zone
Applicable stages: project review, paper design, gray box verification, white box joint debugging, closed testing optimization, season iteration

![Aerial view of border industrial quarantine zone concept](assets/concept-border-industrial-overview.png)

## summary

An extraction map should not be treated only as an arena or a scenic open-world space. Players enter with gear they can lose, search with incomplete information, judge routes, and decide whether to fight. Rewards only matter if the team extracts; death or failed extraction turns the whole run into a loss. The core design task is to make that process learnable, repeatable, and varied enough to keep producing new choices.

In this category, every move of the player has an implicit economic meaning. Taking the main road may reach the high-value area faster, but it will be observed by more players; going around the outer circle may be safer, but time will be consumed and the resource limit is lower; entering the core POI can obtain high-value materials, but it will expose the position, consume ammunition, and attract third parties; the extraction point is not only a safety promise, but also a natural inducement for the end-game conflict. Therefore, map design cannot only discuss "whether it looks good" or "whether there are many routes", but must also discuss search efficiency, encounter probability, sound propagation, AI pressure, evacuation reliability, income density, birth fairness and player learning curve.

This white paper breaks down the search and rescue map into eight levels: category cycle, macro topology, risk-return hotspot, birth evacuation matrix, POI level unit, engagement distance and bunker, PvPvE orchestration, production and telemetry closed loop. The document uses the original map "Border Industrial Quarantine Zone" as a running case, providing implementable design principles, checklists, indicator suggestions and iteration methods. The goal is to help the R&D team reduce structural errors in the paper stage, quickly discover route problems in the gray box stage, and use data to judge the health of the map in the closed and beta stage.

## 1. Category cycle: why map is the core system of search, attack and withdrawal

![Search and withdraw core loop](assets/01-category-loop.svg)

The core cycle of search, strike, and retreat can be summarized into six actions: entry, search, engagement, decision, withdrawal, loss, and growth. The maps of traditional team competitive shooting usually serve the purpose of "fair confrontation". The goals of the battle are clear, and resurrection or round restart will reduce the economic weight of a single death. Search, hit, and withdraw is different. It brings players into a continuous risk account. Instead of just moving around the map, players are betting with their own equipment, time, intelligence and mental capacity.

The map has four responsibilities in this cycle.

First, the map provides revenue targets. Income targets include high-value supplies, mission props, boss drops, safes, key rooms, rare materials, player corpses, information points, and evacuation rewards. Without income targets, players will only treat the map as an arena; if the income is too concentrated, players will be forced to rush to the same hot zone repeatedly. A good search and rescue map will divide the benefits into levels: low-risk areas provide basic supplies, medium-risk areas provide stable benefits, and high-risk areas provide high ceilings and strong narrative memory.

Second, maps produce incomplete information. Players need to know the general direction, but they cannot master all states. Whether there is anyone nearby, whether the boss has been killed, whether an extraction point is available, whether a high-value room has been looted, whether distant gunfire means combat or decoy, this information should be gradually revealed through sounds, landmarks, environmental changes, mission feedback, AI status, and player experience. Too little information can turn into confusion and frustration, and too much information can take away the tension from the risk of withdrawal.

Third, map arrangement conflict probability. Search, fight, and retreat does not require high-intensity firefights in every game, but requires players to believe that conflicts may occur at any time. The map should allow players to understand that certain areas "may be occupied", certain routes "may be blocked", and certain events "will be attractive", but all movements cannot be turned into meaningless random deaths. The design focus of conflict probability is not to distribute evenly, but to allow players to actively adjust risk through route, time, sound, equipment and target selection.

Fourth, maps provide evacuation commitments. The evacuation point is an important spatial structure that distinguishes search and extraction from ordinary survival shooting. It gives players an end to their greed and an outlet for their fears. Extraction points must be reliable enough for players to make plans, but dangerous enough not to be considered free settlement buttons. It is both a security system and an endgame engagement system.

Therefore, the professional design goal of the search, strike and withdrawal map can be written in one sentence: to allow players to continue to face the decision of "be greedier or go now" in a comprehensible space, and allow each choice to be realized by the map, system and economy.

## 2. Macroscopic map structure: topology comes before art, path comes before story

![Macrotopology example](assets/02-macro-topology.svg)

The first step in macro map design is not to draw beautiful terrain, but to determine topological relationships. Topology refers to the connection methods, path costs and conflict relationships between points. A search and rescue map contains at least the following nodes: spawn point, low-risk supply point, medium-risk resource point, high-value hot area, mission point, AI occupation area, condition switch, extraction point, detour channel, observation plateau and sound event source. Art themes can change the presentation of these nodes, but cannot replace their system functions.

Take the "Border Industrial Quarantine Zone" as an example. The map adopts the theme of border industry in the near future. The core area is a blocked experimental factory, and the outer circle consists of a railway warehouse, dormitory area, administrative building, sewage station, dock and wetland. Its structural goal is not to have all players rush towards the Experimental Plant, but to form three main categories of routes.

The first category is high-speed high-risk routes. Players can quickly enter the main road from the spawn point and arrive at the core experimental plant along the container yard, railway bridge or the main entrance of the factory area. This route is short in time and has a high profit ceiling, but the sound exposure is obvious, the probability of early encounter is high, and it is easy to be chased when evacuating. It is suitable for players with high equipment, team players and veterans with clear missions.

The second category is medium-speed controllable routes. Players first search railway warehouses, administrative buildings or sewage stations to obtain supplies, keys, intelligence or mission props, and then decide whether to enter the core area. This type of route provides staged decision points, allowing players to decide whether to "continue to go deeper" or "withdraw with existing profits" in the early and mid-term. It's key to the map's health, as most players shouldn't be forced to make the only correct choice in the opening minutes.

The third category is low-speed conservative routes. Players move along the wetlands, dormitory areas, and outer maintenance lanes. The benefits are low, but they can avoid the core gun line and search for corpses, leftover materials or low-conflict evacuation in the middle and late games. It serves novices, low-gear players, solo queue players, and mission-oriented players. Low-speed routes are not "newbie sanctuaries" but risk modifiers. It gives weaker players room to participate and makes stronger players pay a time penalty in pursuit.

There are three most common mistakes in macro topology design.

First, the center is single-core. All high-value supplies, mission objectives, and bosses are placed in the center of the map, resulting in a highly repetitive route for players, overcrowding in the first ten minutes of the battle, and an empty second half. The central single core is not absolutely unusable, but it must be equipped with outer ring benefits, conditional entrances, delayed events or alternative goals, otherwise the map will be quickly deconstructed into a fixed sprint route by veterans.

Second, the outer circle is meaningless. Many maps will draw a lot of fringe areas, but these areas have no sustainable benefits, no tasks, no observable landmarks, and no tactical value leading to hot zones. Once players learn that the outer circle is a waste of time, they abandon it forever. The outer circle should be responsible for at least one of resupply, detour, retreat, ambush, task collection, or low-risk teaching.

Third, the extraction point is too close to the high-value point. If there is a stable evacuation point next to the core hot zone, players with high equipment will form a high-speed money-spinning line of "rush to the hot zone, get the goods, and leave immediately", which will reduce the activity in the middle and late games of the map. If the extraction point is too far and the route is single, players will feel that success mainly depends on whether they are attacked or not. Evacuation points should maintain a certain spatial distance from high-value areas and be connected through multiple different risk paths.

Macrostructure acceptance can be completed with five questions: whether there are at least two reasonable early routes for each spawn point; whether there are at least three entry directions for each high-value point; whether there are identifiable risk sections for each extraction route; whether the outer circle provides real benefits or tactical value; whether players can find new goals in the middle game, instead of just evacuating or scanning the map.

## 3. Risk and return hot spots: Let value form a pressure field

![Risk-return heat map](assets/03-risk-reward-heatmap.svg)

The value in a search-and-defense map cannot be understood solely in terms of "how many rare materials are placed in the room." What really affects player behavior is the risk-return hotspot. A hot zone is a comprehensive set of signals: high-value supplies, mission objectives, AI strength, sound events, route crossings, evacuation distance, observability, and player expectations. Whether a player is willing to enter a certain area depends on the psychological benefits of superimposing these signals.

A healthy risk-benefit structure should have three levels.

The low-risk, low-return layer provides the basic rhythm. It is located near the spawn point, the outer circle route or the evacuation path, and mainly produces medical treatment, ammunition, ordinary materials, low-level mission props and environmental information. Its function is not to make players rich, but to give players room to start. Novices need to learn landmarks and routes through these areas, and veterans need opportunities to recover when out of gear, injured, or short of ammo.

The medium risk and stable return layer provides the main body of the map. It usually consists of warehouses, dormitories, administrative buildings, small military strongholds, maintenance stations, checkpoints, etc. These areas may not necessarily have the highest value, but they have stable income, diverse routes, and moderate encounter probabilities. The medium-risk tier is the "sustainable content" for search-and-defeat maps, as it determines whether non-top players have enough options.

The high-risk high-reward tier provides memory points. It could be an experimental plant, an underground vault, a boss lair, a signal tower control room, a cordoned off hospital or a large arsenal. It requires strong landmarks, strong narratives, strong benefits and strong costs. High-risk tiers should not be driven solely by “farming more rare supplies,” but should also create costs through entry conditions, noise exposure, AI defenses, spatial oppression, evacuation distance, or competitive missions.

Hot zone design must avoid "implicit unfairness". If players can't see why an area is dangerous, they'll attribute deaths to map malice. If the player sees the danger but chooses to enter anyway, death becomes a replayable price. Visual landmarks, signs of damage, lights, alarms, AI density, distant gunfire, body distribution, and entrance complexity can all convey risk levels.

In the "Border Industrial Quarantine Zone", the core experimental factory is the hottest area. Its red zone not only covers the interior of the building, but also extends to the entrance road, rooftop observation point, power supply station and the outfield that must be passed through for evacuation. Railway warehouses and docks are yellow zones, providing stable income and connecting to main routes. The dormitories and wetlands are green zones that provide medical care, low-level materials, and detour space. Such a hot zone relationship can form three stages: players start from the green zone or yellow zone in the opening game, converge to the red zone or yellow zone in the middle game, and spread from the red zone to the evacuation point in the late game.

Risk-benefit optimization should not only look at the material value, but also record the average stay time, entry rate in the first five minutes, regional mortality, regional visit combination after successful evacuation, player backpack value curve and team size difference. If a certain area has a high visit rate but a very low evacuation success rate, it may be due to excessive punishment; if a certain area has a low visit rate but a high success rate, it may be due to a lack of information guidance; if a certain route has high returns and low mortality, it may be a money-spinning route.

## 4. Birth point and evacuation point: fairness is not equidistant, but optional

![Matrix from birth point to extraction point](assets/04-spawn-extract-matrix.svg)

The spawn point determines the player's starting information, route selection, and early encounter probability. The withdrawal point determines the player's method of cashing out benefits and the pressure at the end of the game. The relationship between the two is often more likely to cause map structural problems than a single POI design.

Many teams will use "the distance from the birth point to the center is about the same" to judge fairness, but the fairness of search, attack and withdrawal is more complicated. One spawn point may be far away from the center, but there are stable supplies and low-risk evacuation nearby, so it is suitable for conservative play; the other spawn point may be close to a high-value point, but it lacks cover and will be flanked by multiple spawn points in the early stage, so the actual risk is higher. Fairness does not mean that all spawn points are exactly the same, but that each spawn point should have explainable advantages, disadvantages, and at least two feasible starts.

There are six principles that should be followed when designing spawn points.

First, avoid fighting each other at birth. Players should not be directly blocked by other spawn points within the first ten to twenty seconds, unless the game clearly pursues a high-pressure hardcore experience and provides strong prompts or cover. The cost of death is high at the start of search, strike and retreat, and conflicts between spawn points will destroy players' trust in the map.

Second, avoid the only optimal route. If a certain birth point naturally corresponds to the shortest high-value route, players will form a fixed running method within a few games, and other choices will be invalid. The only optimum should be broken up by access control, noise, AI, terrain exposure, time cost, or resource scarcity.

Third, ensure that a weak start is guaranteed. The vulnerable spawn point can be far away from the hot area, but it should be nearby low-risk supplies, mission points or safe transfer routes. The guarantee does not mean free income, but ensures that players will not lose the right to participate due to random birth.

Fourth, the extraction point cannot be completely symmetrical. Completely symmetrical extraction points, while seemingly fair, tend to lack narrative and tactical distinction. A better approach is to set up multiple types of evacuation, such as normal evacuation, conditional evacuation, one-time evacuation, paid evacuation, prop evacuation, event evacuation, etc., and let different spawn points face different evacuation plans.

Fifth, the evacuation point must have an anti-crouching point design. Anti-camping is not about canceling the ambush, but making the ambusher pay the price. The evacuation area should be surrounded by multiple entrances, multiple line-of-sight obstructions, alternative routes, countdown exposures, AI patrols, sound signals, or consumable props. Ambush can exist, but it cannot become a low-cost and stable income.

Sixth, the birth-withdrawal relationship requires matrix examination. The design stage should list the distance from each spawn point to each extraction point, the number of main routes, the length of exposed sections, the number of hot zones passed, evacuation conditions and average arrival time. When a combination of "near, high return, low exposure, stable availability" appears in the matrix, additional restrictions must be imposed; when a combination of "far, low return, high exposure, no substitution" appears, compensation must be made.

In the "Border Industrial Isolation Zone", the southwest spawn point is close to the highway, which is suitable for a guaranteed evacuation, but you need to cross the main container road to go to the experimental factory; the northwest spawn point is close to the railway warehouse, and the early income is stable, but evacuation to the dock will cross the hot zone; the southeast spawn point is close to the dock evacuation and sewage station, evacuation is reliable but easy to be observed by the dock high platform; the northeast spawn point is close to the mountain pass for evacuation, the route is safe but the material startup is weak. Such an asymmetric relationship can form different starting characters, instead of making the birth point a copy with only the coordinates different.

## 5. POI level unit: Every high-value point must have an entry script

![POI multiple entrance profile](assets/05-poi-section.svg)

![Concept map of the core experimental plant entrance](assets/concept-core-facility-entrance.png)

POI is the level unit of the search, attack and withdrawal map. Players' memory of the map is often not "I died at coordinates 430,250", but "I was beaten by someone who came in through the side door in the power room on the second floor of the experimental plant." Therefore, POI design determines whether players can form a replayable space experience.

A mature POI must answer at least eight questions: why is it worth visiting; where do players enter from; what can be observed before entering; what will be exposed after entering; how to search inside; how to engage in combat; how to retreat in case of failure; and how to leave after success.

Multiple entrances are a basic requirement for high-value POIs, but multiple entrances do not mean opening more doors. There must be differences for different entrances.

The front entrance is usually the fastest, most intuitive, and easiest to trap. It is suitable for players with high equipment to break through quickly, and it is also suitable for novices to understand the direction of construction. The front door should not be too narrow, otherwise it will become a one-way meat grinder; nor should it be too safe, otherwise it will become the only entrance.

Side gates often connect to bypass routes. It should offer the advantage of lower exposure or closer proximity to specific resource points, but may require longer paths, more complex navigation, or additional acoustic costs. Side doors are an important tool for allowing weaker teams to bypass frontal fire.

Vertical entrances include skylights, stairwells, roofs, underground pipes, elevator shafts and damaged wall openings. Vertical access can significantly increase the tactical depth of a POI, but information asymmetry must be controlled. If the player above has vision, cover, and retreat advantages at the same time, the player below will feel helpless. Vertical entrances should be accompanied by sounds, forward animations, destructibles, or counter-route.

Noise entrances include iron doors, rolling shutter doors, glass, alarms, electric gates, machine doors and water channels. Their value lies in turning "entries" into information events. Players can choose to fast forward, but they must tell those around them that they are here. Noisy entrances are particularly suitable for connecting high-value rooms because they create risk before the benefits are realized.

The exit is not an accessory to the entrance, but key to the POI experience. After the search, attack and withdrawal players get the benefits, their mental state will change from offense to preservation. POI If there is only an entry route but no retreat route, successful players will be forced to return to the original route, which reduces the space strategy. Exit openings can be narrower, more dangerous, and harder to find, but they cannot be missing altogether.

Both extremes should be avoided in POI internal spaces. One is a pure maze, where players are constantly lost in similar corridors and rooms, and cannot be replayed after death. The other is pure lobby, where all combat is determined by long-range sight and there is no tension in the search. A more suitable structure is "identifiable main axis + locally complex rooms + multiple short loops". Spindles help with direction, complex rooms provide search and ambushes, and short loops allow players to flank enemies or retreat.

High-value rooms should have “entry scripts.” For example, there are three ways to enter the core warehouse of the experimental factory: the front door requires a card swipe and will trigger an alarm; the skylight on the second floor needs to be entered from the roof but is exposed to sniper sight; the underground pipes can be bypassed, but the sound of water is obvious and the retreat is slow. All three methods can achieve the same goal, but correspond to different team styles and equipment preparations.

## 6. Line of sight, cover and combat distance: Let the firearms ecology be established in space

![Line of sight and cover indication](assets/06-sightline-cover.svg)

Engagement distance in search-and-defense maps should not be determined solely by gun values. If the map is all long straight roads, snipers and high-magnification lenses will dominate the experience; if it is all indoor short alleys, submachine guns, shotguns, and projectiles will be too powerful; if bunkers are randomly distributed, players will attribute death to luck. Levels need to actively shape the combat ecology at different distances.

The combat distance can be roughly divided into four categories.

The short range is 0 to 15 meters, mainly occurring in rooms, stairs, doorways, container gaps and underground passages. It emphasizes sound judgment, anticipation, throwing objects, opening doors and quick reactions. Close areas are suitable for high-value room entrances, narrow retreats, and high-pressure search spaces, but they cannot cover an excessively large area continuously, otherwise the team’s numerical advantage will be magnified, making it more difficult for single-row players to survive.

The medium and short range is 15 to 35 meters, which is one of the most commonly used engagement stages for search, attack and withdrawal. It allows submachine guns, rifles, shotguns, and semi-automatic weapons to all participate, and also allows players to use bunkers for displacement. Warehouses, courtyards, dormitory building intervals, pipe corridors and small blocks are all suitable for this distance segment.

Medium and long range 35 to 80 meters, suitable for rifle suppression, observation and transfer. This distance allows players to feel like the map is open, but still has the opportunity to react through cover, smoke, route selection, and retreat. This distance segment can be used on industrial park roads, railway yards, dock yards and hillside edges.

Long range of more than 80 meters, suitable for sniping, reconnaissance and area deterrence. Long-range line of sight should be used with caution, especially if it cannot continuously cover the spawn point, extraction point and main route. Long sightlines must be offset by costs such as exposure of the shooter's position, difficulty in retreat, scarcity of supplies, weather-impaired sightlines, or the need to give up high-value search time.

Bunkers also need to be layered. Hard cover can block bullets and provide a stable combat rhythm; soft cover can block sight but not necessarily damage, creating uncertainty in information; half-body cover provides posture selection; penetrable cover increases the knowledge gap; and destructible cover provides dynamic changes. The visual language of different bunkers must be clear, and players need to be able to judge "can there be life here" under high pressure?

Search, attack and withdrawal particularly require "retreat bunkers". Traditional competitive maps focus more on attack routes and firefighting points, while search-and-fight players often choose to retreat after receiving benefits. If there are no intermittent bunkers on the retreat route, players will be chased by long lines of sight without solution; if the retreat route is too densely covered with bunkers, the pursuers will lack opportunities. A reasonable approach is to set up rhythmic cover: give short pauses every 15 to 30 meters, but create windows of exposure in key corners or open sections.

Sound is the other half of sight. Metal pedals, broken glass, puddles, iron doors, alarms, elevators, turnstiles and generators in industrial maps can all become level mechanisms. Sound material is more than just ambience, it can change player pathing. If a shortcut inevitably involves stepping on a tin roof, the player understands the cost when choosing it. If a high-value room is broadcast to the whole area when it is opened, the battle will no longer be a random encounter, but will revolve around information events.

## 7. PvPvE orchestration: AI is not a filler, but a risk pacer

Search-and-defeat PvPvE isn't about simply placing a few enemies on the map. There are at least five functions of AI: guarding profits, making sound, consuming resources, exposing players, and changing routes. If the AI ​​only stands next to the supply box and waits for players to clean it up, it will quickly turn into a money-spinning process; if the AI ​​is too precise, too numerous, and refreshed too frequently, it will overwhelm PvP judgment and make players feel that they are mainly fighting the system.

AI footprints should serve the map hierarchy. A small amount of weak AI can be placed in low-risk areas to teach sounds, enemy detection, and basic combat. Medium-risk areas can be placed with patrol AI or squad AI, allowing players to clear or detour. High-risk areas can house elite AI, bosses, turrets, drones, alarm systems, or reinforcement mechanisms, forcing players to prepare before entering.

Boss design is especially tied to the map structure. The boss shouldn't just be a high-health enemy, but the centerpiece of the zone's events. It can change access control, trigger broadcasts, enable special evacuation, drop keys, attract AI reinforcements, or alter local electricity. The information after the boss is killed should be perceived by other players in some way, forming a third-party competition. According to public information, the bounty and clue mechanism of Hunt: Showdown reflects the design idea of ​​"target advancement will change the global information"; players use clues to narrow the scope of the target, and after picking up the bounty, they will also expose their own pressure. Search, Strike, and Defeat won't necessarily copy this mechanic, but it should learn from the way it ties together PvE objectives, map information, and player conflict.

The value of AI voice is often underestimated. When a player shoots to clear the AI, he not only consumes ammunition, but also tells the surrounding players his approximate location, weapon type, fighting direction, and risk status. If AI can force players to speak out, it can transform maps from static spaces into information networks. Conversely, if large numbers of AI are costlessly dealt with by silenced weapons, or the sound of AI and player battles cannot be propagated, the linkage value of PvPvE will decrease.

Be careful with AI refreshes. Search, strike and retreat emphasizes learnability, and players need to believe that there are threats in certain areas. Completely random AI farming will reduce the review value; completely fixed AI farming will be scripted by the farming route. A better way is "fixed area + random combination + conditional reinforcements". For example, the Core Experimental Factory always has defensive forces, but the specific patrol routes, elite unit locations, and reinforcement triggering conditions will change.

The relationship between AI and extraction points is also worth designing. There can be a small number of patrolling AI in the evacuation area to prevent long-term squatting, or the search team can be refreshed after high-value events to force players carrying high-value supplies to speed up their decision-making. However, the evacuation AI cannot be strong enough to replace the player's threat, otherwise players will feel that evacuation failure mainly comes from system punishment.

## 8. Search and economic distribution: turning materials into route language

The material distribution of search, attack and evacuation is not the end execution of the value table, but the core language of map design. Players learn the map through materials: where is suitable for replenishing medical treatment, where is suitable for finding gun accessories, where is it possible to obtain mission props, where is it worth using keys, and where has it been searched. The distribution of supplies determines whether players will explore the map repeatedly or only remember a few high-value boxes.

Materials should be distinguished by "stability" and "upper limit". Stable income is suitable for medium and low-risk areas to help players form reliable routes; high-cap income is suitable for high-risk areas to create competition and emotional peaks. The stable income does not have to be high, but it should make players feel that their time is not wasted. High-cap income does not have to appear every game, but when it does it should be enough to change the player's decision-making.

Mission props and economic materials should be separated but related. If all tasks require entering the highest hot zone, novice and low-equipment players will be forced into a high-pressure environment; if all tasks are completed in the outer circle, task players will be separated from the main body of PvP. A more reasonable approach is to let the task chain guide gradually: early tasks learn the outer circle and evacuation, mid-term tasks enter the medium-risk zone, and later tasks touch the core hot zone. Quest items allow players to understand the route rather than just being a checklist collectible.

Key rooms and safes are classic risk-benefit amplifiers. They shouldn't be just skin for a high-value box, but should come with preparation costs, routing, and sonic penalties. Keys may take up backpack or safe space, opening doors may trigger sounds, rooms may lack safe exits, or power may need to be turned on in another part of the map first. In this way, the key room will change from a "money point" to a "plan target".

The readability of supply containers is important. Players should be able to infer supply categories based on container type, area theme, and environmental narrative. Medical care comes out of the medical cabinet, weapon accessories come out of the ordnance box, intelligence and electronic materials come out of the office, living supplies come out of the dormitory, and rare samples come out of the experimental factory. A completely random supply list will weaken map learning; over-fixation will make the route rigid. It is recommended to adopt the principle of “stable category, fluctuating quality, and few surprises”.

Economic distribution also takes into account team differences. Teams of three are better at clearing high-risk areas and can carry more loot. If high-value supplies are concentrated and can be evacuated quickly, the advantage of teamwork will be further magnified. Single point evacuation issues should be mitigated through weight, container opening time, multiple dispersed targets, conditional evacuation, noise events, and task mutual exclusion. Solo players do not need to have exactly the same benefits as a three-player team, but there should be a low-noise, high-judgment route suitable for solo queue.

The key indicators of the map economy include: the average value brought out per unit time, the evacuation success rate after area visits, the income gap between different team sizes, the key room opening rate, the flow of high-value materials, the value of the backpack when the player dies, the guaranteed area access rate, the empty-handed evacuation rate and the continuous failure rate of low-equipment players. If the economic data only looks at the overall average, it can easily hide that some routes are too strong or some player levels are overwhelmed.

## 9. Information, navigation and learning curve: hardcore does not mean not telling players

Search, fight, and retreat players can accept risks, but it is difficult to accept unlearnable chaos for a long time. The more hard-core the map, the more reliable information design is needed. Rather than having all objectives marked on the UI, navigation lets players model the space through landmarks, routes, sounds, architectural language, and mission text.

Landmark design should be divided into three layers. Distant landmarks are used to determine the general direction, such as experimental plant chimneys, radar towers, mountain pass lighthouses, and port cranes. Mid-ground landmarks are used for route selection, such as railway bridges, red warehouses, sewage treatment tanks, and dormitory buildings. Close-up landmarks are used for local battles, such as broken stairs, blue iron doors, generator rooms, and collapsed wall holes. The three layers of landmarks together help players transition from "where am I" to "how should I go" and "where the enemy may come from".

The strength of the map UI should be consistent with the project positioning. Hardcore projects may not display real-time player locations, but should still provide high-quality paper maps, extraction point names, landmark consistency, and mission text. Popular projects can provide simplified maps, direction tips, evacuation condition tips and teammate marks. Whichever strength you choose, avoid inconsistent information rules. Players don’t have to know everything, but they must know the rules according to which the system hides information.

Evacuation tips are especially important. Extraction points can be conditional, but the conditions must be understandable. For example, "the sewage station gate needs to be turned on", "border pass required", "will only open after a 20-minute countdown" and "disposable vehicle evacuation". If the reason for an evacuation failure is unclear, players will attribute the failure to a bug or malicious design. Visual, audio, and UI feedback for extraction points should be clear.

The cost of black box learning needs to be controlled. One of the charms of Search and Fight is that players will learn the map through death, but not all knowledge is suitable for teaching through death. Which windows can be climbed, which fences can be penetrated, which bodies of water slow down, which doors can be opened, which walls can be penetrated, these rules should have a stable visual language. Unpredictable interaction rules can turn map learning into a memory burden.

The novice guide can be hidden in the map instead of being a separate tutorial. Low-risk areas should display basic supply containers, simple AI, obvious evacuation points, and clear landmarks. Medium risk areas display detours, noise entrances, key rooms, and intersecting routes. High-risk zones showcase complex verticals, strong AI, public events, and evacuation pressure. In this way, the player's growth path will naturally be consistent with the depth of the map.

## 10. Anti-crouching and fairness: Ambushes are allowed, but ambush must have costs

Search, attack and retreat must allow ambush. If ambushes were eliminated entirely, the tension of evacuation would be reduced and the information game would be reduced. But ambush cannot be turned into a low-cost, low-risk, high-stable return strategy. The goal of anti-crouching point design is not to make every extraction point absolutely safe, but to make ambushers have to invest time, expose their position, and bear the risk of being bypassed or interfered by AI.

Evacuation and squatting usually come from four problems: the evacuation point has a single entrance, the observation point is too strong, players cannot move during the evacuation countdown, and there is a lack of alternative routes around the evacuation point. Correction methods include adding multiple entrance evacuation areas, setting up short-term sound exposure, providing smoke or cover, making the evacuation countdown interruptible, making the crouching position lack supplies, adding patrol AI, designing anti-observation routes, or setting up conditional evacuation.

Spawn squatting comes from early route overlap. If the two spawn points naturally rush to the same resource point along the same main road, the veteran will hold each other at a fixed time point. The solution is not to simply move the spawn point farther away, but to increase early route bifurcation, obscure the initial line of sight, adjust resource incentives, delay the opening of high-value points, or allow multiple spawn points to have different but equivalent early goals.

The reason for squatting in hot areas is that there are too few ways to realize profits. After the player obtains high-value supplies, if they can only leave through the same stairs, the same door, and the same bridge, the ambusher can wait at a low cost. Exit routes in high-value areas should have at least two options with different costs: fast but exposed, slow but concealed, safe but requiring props, or dangerous but able to bypass the main road.

Sound squatting also needs attention. If certain material sounds are too obvious and unavoidable, veterans will overpower newbies with their sounds for a long time. Sound should provide information, but also give the player choices. For example, the waterway is slow but hidden, the iron bridge is fast but noisy, the grassland is quiet but has poor visibility, and the glass shortcut is fast but will break and alarm. Sound shouldn't just be punishment, it should also be route strategy.

Fairness ultimately comes back to replayability. If a player can say after death, "I took advantage of the core warehouse, did not check the freight elevator door, and took sight of the high platform when evacuating," this is a health failure. If the player can only say "I was killed by someone who didn't know where I was just after I was born" or "There are always people squatting at the extraction point", this is a structural problem.

## 11. Pressure during the evacuation phase: Time must be used to manage actions, not just to end the war.

![Evacuation phase pressure curve](assets/07-extraction-pressure-curve.svg)

![Pier evacuation point concept map](assets/concept-extraction-checkpoint.png)

The time system for search, attack and withdrawal cannot be understood as just a countdown. A countdown will certainly force players to evacuate, but a truly professional map will allow time to change the behavior of space. The opening, middle game, and late game should have different route values, information density, and conflict patterns.

The core of the opening stage is route differentiation. When players are first born, they have complete equipment, little information, and zero income. The most common behavior is to quickly determine nearby targets. It is not advisable to overpress at this stage, otherwise players will enter the crossfire before they have made a decision. The map should provide clear landmarks, nearby supplies, early forks, and a small amount of low-intensity AI, allowing players to choose to rush into hot zones, search the outer circle, or complete tasks.

The core of the middle game stage is information diffusion. Gunshots, alarms, boss status, opened doors, searched containers, and player corpses will gradually tell other players what is happening on the map. The midgame doesn't need to force everyone to meet, but it should give players reasons to change their original plans through high-value events, conditional switches, and route crossovers.

The core of the post-game stage is the realization of profits. Players begin to move towards the extraction point, the value of backpacks increases, ammunition and health decrease, and the mentality shifts from greed to preservation. At this point, the map can increase pressure through extraction point countdowns, weather changes, AI patrols, public events, or conditional extraction closures, but it cannot allow the end game to become random punishment. Pressure should come from map rules that players can understand.

The back-end design of the border industrial quarantine zone can use two sets of light events, namely heavy rain enhancement and border patrol. Heavy rain reduces long-range vision and increases the weight of near- and mid-range combat; patrols compress completely safe outer routes, but will not directly cover all evacuation points. In this way, there will be changes in the later game, but it will not negate the evacuation plan made by the players in the early stage.

## 12. Original Case: Complete Design Draft of Border Industrial Quarantine Zone

Border Industrial Quarantine is a medium-to-large search-and-fight map for 24 to 36 players, supporting solo to three-person teams. The recommended length of a single session is 35 to 45 minutes. The theme of the map is a blocked industrial experimental zone next to the border. After an accident, the area was contested by military contractors, smugglers and scavengers. The setting serves three design purposes: industrial facilities provide clear landmarks and complex interior spaces; borders provide evacuation and blockade narratives; quarantine incidents provide PvE threats, rare samples, and dynamic events.

The map is divided into six main areas.

The core experimental plant is the highest value area and is located in the north-central part of the map. It consists of a three-story main building, an underground sample library, a roof ventilation platform, a power room, an alarm door and a freight elevator. Core benefits include rare samples, electronic components, advanced medical, mission files, and boss drops. The main risks come from strong AI, defensive turrets, alarm broadcasts, multiple entrances for flanking, and evacuation distance.

The railway warehouse is located in the middle of the west side and is a medium-risk and stable profit area. It provides weapon accessories, industrial materials, mission props and mid-range engagement space. The railway warehouse connects the northwest spawn point, the southwest main road and the experimental factory outfield. Its function is to allow players on the west side to have staged goals instead of being forced to rush straight to the center.

The sewage station is located in the middle of the east side and is a medium risk control area. Here players can open some underground doors, turn off certain alarms, or activate conditional evacuation. The sewage station is not the most profitable, but it has systemic value and can change subsequent routes. It's suitable for making battles revolve around "control".

The dormitory area is located in the south and is a low to medium risk supply area. It provides medical treatment, food, low-level materials, living supplies and task collection. The dormitory area has a high building density and a short combat distance, making it suitable for novices to learn indoor search and retreat. The dormitory area is connected to the highway for evacuation and is a guaranteed area for players with low equipment.

The terminal yard is located in the southeast and is a medium- and high-risk evacuation competition area. It contains containers, cranes, warehouses and waterways. The dock has both stable supplies and evacuation points, so it is easy to form mid- and late-game battles. The yard requires a large number of soft shelters and multi-layer routes to avoid one-way suppression from high platforms.

The outer circle of wetlands and borders is located on the southwestern and northeastern edges of the map and is a low-risk detour and reconnaissance area. It has low yield, but avoids the central trunk line and provides some hidden missions and sniper observation points. The moving speed of the wetland is slightly slower, the sound is lower, and the vision is affected by reeds, rain and fog.

There are four categories of evacuation points. Highway evacuation is stable and open, but far away from the core hot area; dock evacuation requires waiting for vehicles, and there is sound exposure during the countdown; mountain pass evacuation is suitable for players on the north side, but the route is narrow and easy to be observed; conditional evacuation requires a sewage station switch or experimental plant pass, which is closer to high-value areas but has clear upfront costs.

There are three types of dynamic events. The first is the experimental factory alarm. When the player opens the core sample library, the entire area will hear the alarm and refresh AI reinforcements. The second is border patrol. Patrol teams appear in the outer circle in the middle and late stages of the game to compress the overly safe edge routes. The third is that the heavy rain intensifies, the sound of rain becomes stronger in the later stages, the long-distance sight line decreases, and the sound of metal materials becomes more prominent, which changes the engagement method during the evacuation phase.

The objective experience of this map can be divided into three player stories.

Traditional players start from the dormitory area or the outer circle, collect basic materials, hear the gunshots from the experimental factory, go around to the railway warehouse to pick up leaks, and finally evacuate from the highway. The story offers low-gear engagement.

Enterprising players rush into the railway warehouse or sewage station at the beginning. After getting the key or control, they enter the experimental factory, clean the core warehouse, trigger the alarm, and move to the dock with high-value materials or evacuate under conditions. This story offers high-voltage earnings spikes.

Hunter players are not in a hurry to search, but judge the routes of other teams based on gunshots and alarms, ambush players evacuating from the experimental factory in the middle game, and then choose whether to risk searching for corpses or evacuate quickly. This story provides a PvP informative game.

If all three stories can be established on the same map, it means that the map is not just a space, but a system that can repeatedly generate different situations.

## 13. Production method: closed loop from gray box to telemetry

![Map level production pipeline](assets/08-production-pipeline.svg)

Search, strike, and withdraw map production is not suitable for making high-quality art first and then adjusting the gameplay. The reason is straightforward: the coupling of paths, lines of sight, evacuation, supplies, and AI is too strong. Once the art assets are finalized, subsequent modification costs will be extremely high. It is recommended to adopt a five-stage pipeline: paper design, gray box verification, white box joint debugging, sealing and testing telemetry, and operation iteration.

The paper design phase outputs map topology, area positioning, spawn evacuation matrix, POI hierarchy, risk-benefit assumptions, and key player stories. Don’t get obsessed with detailed rooms at this stage, but confirm whether the map has enough effective routes and staged options.

The gray box verification phase uses simple geometry to build a map, focusing on testing route duration, line of sight length, bunker rhythm, birth conflicts, evacuation campsites, and POI multiple entrances. The goal of the gray box phase is not to look good, but to quickly overturn incorrect assumptions. Each test should record the player's starting route, first encounter time, first death location, extraction route, and subjective point of confusion.

In the white box joint debugging stage, basic art, AI, materials, tasks, audio, interactive doors, evacuation logic and performance budget are added. At this stage, special attention should be paid to the mutual amplification between systems. For example, a certain high-value room may be reasonable without AI, but excessively punished after adding alarms and bosses; a certain route may not be taken by anyone when there are no supplies, but adding mission props will cause birth conflicts.

Map health indicators need to be established during the closed beta telemetry phase. It is recommended to record at least: area visit rate, area death rate, average first encounter time, evacuation success rate, usage rate of different evacuation points, value brought out by players, backpack value at death, team size profit difference, evacuation rate after boss kill, key room opening rate, spawn point survival rate, kill rate near evacuation point, player stay heat map and route traffic.

Don’t just adjust material values ​​during the operation iteration phase. Many economic problems are essentially route problems, many combat problems are essentially line of sight problems, and many novice losses are essentially navigation problems. Iterations should give priority to determining the type of problem: if a certain area has high profits and low death, it may be necessary to increase exposure, extend the evacuation distance, or reduce refresh; if a certain area has high death and low profits, it may be necessary to add bunkers, add alternative routes, or increase profits; if a certain evacuation point has an abnormally high kill rate, it may be necessary to increase anti-crouching routes, adjust the countdown, or change observation points.

## 14. Professional acceptance checklist

The following checklist can be used for review meetings, gray box milestones, and closed beta reviews.

Macrostructure inspection:

| Inspection items | Qualification standards | Risk signals |
| --- | --- | --- |
| Spawn point | Each spawn point has at least two possible openings | Frequent fights within 30 seconds of birth |
| Main route | The main route is clear but not unique | Players highly repeat the same route |
| Outer circle route | Has supply, mission, detour or retreat value | Outer circle access rate has been too low for a long time |
| High value area | At least three entry directions and two retreat directions | Single door, single bridge and single staircase become the meat grinding point |
| Evacuation point | Stable evacuation and conditional evacuation coexist | The kill rate of a certain evacuation point is abnormally high |

POI check:

| Inspection items | Qualification standards | Risk signals |
| --- | --- | --- |
| Differences in entrance | Fast entrance, concealed entrance, noise entrance, and vertical entrance have different prices | Multiple entrances but the same experience |
| Search rhythm | The main axis is clear, the room has local complexity | Pure maze or pure hall |
| Sound events | High-value actions generate information | Players take away the highest benefits silently |
| Escape route | There is more than one way to leave after success | Return the same way and be ambushed |
| Readability | Materials, doors, windows, and wall rules are stable | Players cannot judge whether they can interact or penetrate |

Combat check:

| Inspection items | Qualification standards | Risk signals |
| --- | --- | --- |
| Combat distance | There are corresponding areas for near, medium and long range | A single firearm type dominates the map |
| Long line of sight | Costly and counter-route | Long line of sight continuously covers birth or evacuation |
| Bunker rhythm | There are staged bunkers for both advancement and retreat | There is no solution in the open area or the bunkers are too dense |
| Vertical space | Both high and low positions have information costs | High positions also have vision, cover, and retreat |
| Sound materials | Sound can guide route selection | Sound punishment cannot be avoided |

Financial Check:

| Inspection items | Qualification standards | Risk signals |
| --- | --- | --- |
| Low-risk returns | Can support guaranteed participation | Low-equipment players continue to fail empty-handed |
| Medium risk return | Stable and diverse routes | Players skip the middle level and go straight to the red zone |
| High-risk returns | High upper limit but clear price | Rapid money-spinning line is stably formed |
| Task distribution | Step by step guide to map learning | Early tasks are forced into the hottest areas |
| Team differences | There are feasible routes for solo queues, and high-pressure goals for teams | A three-person team monopolizes all high-value resources |

Telemetry check:

| Metrics | Design Implications |
| --- | --- |
| First encounter time | Determine whether the opening is overcrowded or empty |
| Regional mortality | Determine whether the pressure in hot areas is reasonable |
| Regional visit rate | Determine whether landmarks, tasks and revenue guidance are effective |
| Evacuation success rate | Determine whether the risk-return closed loop is healthy |
| Kill rate near the evacuation point | Determine whether the evacuation squat is too strong |
| Bring value per unit time | Determine whether the money-spinning route is unbalanced |
| Birth point survival rate | Determine the fairness of birth |
| Team size return difference | Determine whether the team advantage is over-amplified |

## 15. Frequently Asked Questions and Corrections

Problem 1: Players always hit the same center point.
Possible reasons are that the center income is too high, the outer circle is worthless, the tasks are concentrated, the evacuation is too close, or there are too few routes. Correction methods include increasing the value of tasks in the outer circle, giving stable benefits to medium-risk areas, delaying the opening of high-value centers, increasing the evacuation distance of the center, or making the center benefits require preconditions for other areas.

Question 2: Players always say that the map is too spacey.
It's not necessarily that the map is too large, it could be that the route lacks objectives, insufficient sound propagation, weak landmarks, sparse AI, or insufficient midgame events. Correction methods include adding medium-risk POIs, adding audible events, improving route intersection quality, adding corpses and battle traces, or setting dynamic goals in the game.

Question 3: Players always say that the map is too messy.
It may be that the landmark hierarchy is unclear, indoor duplication, routes are too densely intersecting, entrance rules are unstable, or UI information is insufficient. Correction methods include strengthening distant landmarks, reducing similar rooms, clarifying the main axis route, unifying the language of doors and windows, and optimizing task texts and evacuation prompts.

Problem 4: The evacuation point is often squatted.
It may be that there is a single evacuation entrance, the observation point is too strong, the countdown is too long, there is no cost to crouching in the position, or there are too few alternative evacuation options. Correction methods include adding cover and rewind routes, adjusting observation heights, adding sound or AI pressure to the crouching position, changing the evacuation countdown, and adding conditional evacuation.

Problem 5: The high-equipment team snowballs.
It could be that high-value areas can be cleared quickly, the evacuation is too close, the AI ​​does not put enough pressure on the team, the weight of supplies is low, or there are few alternative routes for single rows. Correction methods include dispersing high-value targets, increasing transportation costs, setting up multi-stage events, increasing the exposure of strong teams, and providing low-noise targets for single platoons.

Problem 6: Newbies don’t know what to do.
It may be that the low-risk area lacks clear goals, the map landmarks are unclear, the evacuation rules are difficult to understand, and the task text does not point to spatial learning. Corrections include having readable supplies and simpler AI near spawns, strengthening distant landmarks, and guiding players through a low-risk search and extraction in early missions.

## 16. Design inspiration from competing product references

This report does not embed screenshots of competing products, but only discusses the inspiration at the public mechanism level.

Escape from Tarkov's core inspiration for the category is that gear loss, map knowledge, and high-value supplies all work together to shape a long-term learning curve. The player's mastery of the map will directly affect the survival rate and profitability, which shows that search, attack and withdrawal maps require stable enough spatial rules to make the accumulation of knowledge valuable.

The inspiration for Hunt: Showdown lies in the binding of objective information and player conflict. The official manual emphasizes that clues, bosses, bounties, and evacuation together form the round goal chain. It does not allow all players to fight randomly, but gradually pulls players into a shared pressure field through goal advancement.

Delta Force's Operations direction has reference significance for more popular search, attack and extraction: map tools, tactical information, asset search and evacuation targets can lower the entry barrier. For projects looking to expand their user base, information presentation and map readability should not be viewed simply as “reducing hardcoreness,” but rather as a means of reducing pointless frustration.

GDC multiplayer level design materials repeatedly emphasize the importance of gray boxes, feedback, pacing, and observation of player behavior. This approach is especially needed for search-and-defeat maps, because many problems are only exposed through real route selection, real economic pressure, and real team behavior. A route that makes sense on paper can be completely thrown off balance by a long sight line, a high-value box, or a countdown to an extraction point.

## 17. Conclusion: Search, strike and withdraw map is an operational risk system

Professional search and rescue map design is not to fill a complex scene with supplies and enemies, but to establish a stable, readable, gameable, and adjustable risk system. The map allows players to understand where the danger is, why it is dangerous, what can be gained by entering the danger, and what has to be paid to leave the danger. The level should allow each POI to have entry scripts, search rhythms, engagement structures, and retreat options. The system requires materials, AI, tasks, sounds, and evacuation to jointly drive player decision-making. Operations should use data to continuously verify these assumptions.

The case of "Border Industrial Quarantine Zone" illustrates that a search and rescue map can simultaneously support three types of player stories: conservative search, aggressive penetration, and hunter interception. The key is not how big the map is, but that every route has a clear cost, every hot zone has readable incentives, every evacuation option has pressure, and every failure can be transformed into a better judgment next time.

Ultimately, the highest goal of searching, attacking, and withdrawing maps is not to allow players to win every game, nor to allow players to complete every game, but to make players willing to review the game after leaving the battle: "If I had just changed a route, retreated earlier, opened the door later, and listened to the sound first, the results may have been different." As long as the map can continue to create such repeatable regrets and plans for the next game, it will have long-term vitality.

## Figure And Source Notes

All figures in the main text are local assets. They help readers understand topology, risk and reward, POI entrances, sightlines and cover, extraction pressure, and the production pipeline. They are level-design diagrams, not competitor screenshots, official scale maps, or real telemetry results. Public product references and methodology sources are collected in the next section.

## References

- [Hunt: Showdown Official Manual](https://www.huntshowdown.com/manual)
- [Delta Force Maps Wiki](https://www.playdeltaforce.com/act/mapswiki/?lang=en)
- [GDC Vault - Level Design Workshop: The Holy Grail](https://www.gdcvault.com/play/1025183/Level-Design-Workshop-The-Holy)
- [GDC Vault - Level Design Fundamentals](https://gdcvault.com/play/1022456/Level-Design-Fundamentals)
- [Escape from Tarkov Official Website](https://www.escapefromtarkov.com/)
