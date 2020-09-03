# ensweaterator pseudocode 

## ensweaterator specs
the ensweaterator is a solar-powered autonomous vehicle that performs the following functions:
* rolls autonomously around city streets
    * uses self-driving technology shamelessly stolen from unnamed tech giants
* carries knitting materials
    * 20-kilo yarn cone
* carries drone-enabled knitting tools
    * needle bed
    * yarn carriage
* identifies people who are cold
    * uses thermal imaging (:copyright: Austin)
* knits sweaters directly onto the bodies of the cold people it has identified
    * plays looping warning message
        * "WARNING! YOU ARE BEING ENSWEATERATED! PLEASE HOLD YOUR ARMS STRAIGHT OUT AND STAND PERFECTLY STILL!
    * runs AI trained on open-source pictures of bodies (mostly human, i think) to identify body parts

## ensweaterator program
```
PROGRAM ensweaterate

OBJECTS/FUNCTIONS

vehicle
    sleep
    wander
    find-cold-person
    play-warning-message
    eject(knit-drone)
    pack-up(knit-drone)

cold-person
    stand-still-with-arms-out
cold-person#hips
cold-person#armpits
cold-person#collarbone
cold-person#arm
cold-person#arm#wrist

knit-drone
    find(body-part)
    assemble-needle-band(body-part-location)
    cast-on
    knit-around
    split-needle-band
    knit-flat
    cut-yarn
    disassemble-needle-band
    switch-sides
    pick-up-stitches
    seam-shoulders
    bind-off
knit-drone#needle-band

yarn
    run-out

INIT {
    create-vehicle
    create-cold-person
    create-knit-drone
    create-yarn
}

WHILE NOT yarn
    vehicle.sleep

WHILE NOT cold-person
    vehicle.wander
    vehicle.find-cold-person

WHILE cold-person
    // prepare to knit
    vehicle.play-warning-message
    vehicle.eject(knit-drone)
    knit-drone.find(cold-person#hips)
    knit-drone.find(cold-person#armpits)
    knit-drone.assemble-needle-band(cold-person#hips)
    // knit the sweater body
    knit-drone.cast-on
    WHILE knit-drone#needle-band != cold-person#armpits
        knit-drone.knit-around
    knit-drone.find(cold-person#collarbone)
    knit-drone.split-needle-band
    WHILE needle-band != cold-person#collarbone
        knit-drone.knit-flat
    knit-drone.cut-yarn
    knit-drone.switch-sides
    knit-drone.pick-up-stitches
    WHILE knit-drone#needle-band != cold-person#collarbone
        knit-drone.knit-flat
    knit-drone.cut-yarn
    knit-drone.seam-shoulders
    knit-drone.disassemble-needle-band
    // knit the sleeves
    knit-drone.find(cold-person#arms)
    FOR arm in cold-person#arms:
        knit-drone.find(arm#wrist)
        knit-drone.assemble-needle-band(arm)
        knit-drone.cast-on
        WHILE needle-band != arm#wrist
            knit-drone.knit-around
        knit-drone.bind-off
        knit-drone.cut-yarn
        knit-drone.disassemble-needle-band
    vehicle.pack-up(knit-drone)
    cold-person := warm-person

EXCEPT
    IF
        yarn.run-out
    THEN
        vehicle.pack-up(knit-drone)
        vehicle.sleep
    ELSE IF
        NOT cold-person.stand-still-with-arms-out
    THEN
        knit-drone.cut-yarn
        knit-drone.disassemble-needle-band
        vehicle.pack-up(knit-drone)
        vehicle.wander
        vehicle.find-cold-person

END
```