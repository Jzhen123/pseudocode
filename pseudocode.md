# ensweaterator pseudocode 

## ensweaterator specs
the ensweaterator is a solar-powered autonomous vehicle that performs the following functions:
* rolls autonomously around city streets
    * uses self-driving technology shamelessly stolen from an unnamed tech giant
* carries knitting materials
    * 20-kilogram cone of yarn
* carries drone-enabled machine-knitting tools
    * needle band & yarn carriage
* identifies people who are cold
    * uses thermal imaging (:copyright: Austin)
* knits sweaters directly onto the bodies of the cold people it has identified
    * plays looping warning message
        * "WARNING! YOU ARE BEING ENSWEATERATED! HOLD YOUR ARMS OUT STRAIGHT AND STAND PERFECTLY STILL!"
    * runs AI trained on open-source pictures of bodies (mostly human, i think) to identify body parts

## ensweaterator program
```
PROGRAM ensweaterate

// define objects & functions

vehicle
    sleep() // power down and wait for a technician to refill yarn and restart
    wander() // roll slowly along city sidewalks
    find-cold-person(visual-input) // search visual field for objects that appear to be human and cold; return cold-person
    play-warning() // play a recording telling a cold person how to cooperate with ensweateration
    eject(knit-drone) // release the knit drone to begin ensweateration
    pack-up(knit-drone) // load the knit drone back into the vehicle after ensweateration

cold-person
    stand-still-with-arms-out() // what a cooperative cold person must do to be ensweaterated safely
cold-person#hips
cold-person#armpits
cold-person#collarbone
cold-person#neck-left
cold-person#neck-right
cold-person#shoulder-left
cold-person#shoulder-right
cold-person#wrist-left
cold-person#wrist-right

knit-drone
    find(cold-person#body-part) // return location of given body part
    assemble-needle-band(cold-person#body-part-start#location,cold-person#body-part-end#location) // prepare the needle band for knitting at the start location, oriented toward the end location, and attach yarn carriage
    cast-on() // attach yarn to needle band using yarn carriage
    knit-around(cold-person#body-part#location) // move yarn carriage for one complete rotation around needle band, then move needle band 0.5cm (the height of one knitted row) toward the given location
    split-needle-band() // split the round needle band evenly into two flat needle bands
    knit-flat(cold-person#body-part#location) // move yarn carriage from one end of the flat needle band to another, then move needle band 0.5cm (the height of one knitted row) toward the given location
    switch-sides() // move the yarn carriage from one side of the split needle band to the other
    cut-yarn() // cut the yarn 10cm away from where it is currently attached to the needle band
    disassemble-needle-band() // separate the components of the needle band and bring them away from the cold person's body
    seam(cold-person#body-part-start#location,cold-person#body-part-end#location) // join and bind off stitches from the two sides of the needle band, from the start location to the end location
    pick-up-stitches(cold-person#body-part#location) // insert needles on needle band into fabric at the given location
    bind-off() // catch and detach all stitches along the needle band
knit-drone#needle-band

yarn
    run-out() // yarn carriage reaches yarn end without cutting it

// deploy the ensweaterator

INIT {
    create-vehicle
    create-knit-drone
    create-yarn
}

WHILE NOT yarn
    vehicle.sleep()

WHILE NOT cold-person
    vehicle.wander()
    vehicle.find-cold-person(visual-input)

WHILE cold-person

    // prepare to knit
    vehicle.play-warning()
    vehicle.eject(knit-drone)
    knit-drone.find(cold-person#hips)
    knit-drone.find(cold-person#armpits)
    knit-drone.assemble-needle-band(cold-person#hips#location,cold-person#armpits#location)

    // knit the sweater body
    knit-drone.cast-on()
    WHILE knit-drone#needle-band#location != cold-person#armpits#location
        knit-drone.knit-around(cold-person#armpits#location)
    knit-drone.find(cold-person#collarbone)
    knit-drone.split-needle-band()
    WHILE knit-drone#needle-band#location != cold-person#collarbone#location
        knit-drone.knit-flat(cold-person#collarbone#location)
    knit-drone.cut-yarn()
    knit-drone.switch-sides()
    WHILE knit-drone#needle-band#location != cold-person#collarbone#location
        knit-drone.knit-flat(cold-person#collarbone#location)
    knit-drone.cut-yarn()

    // seam the sweater's shoulders
    FOR SIDE in [left,right]
        knit-drone.find(cold-person#shoulder-SIDE)
        knit-drone.find(cold-person#neck-SIDE)
        knit-drone.seam(cold-person#shoulder-SIDE#location,cold-person#neck-SIDE#location)
    knit-drone.disassemble-needle-band()

    // knit the sleeves
    FOR SIDE in [left,right]:
        knit-drone.find(cold-person#wrist-SIDE)
        knit-drone.assemble-needle-band(cold-person#shoulder-SIDE#location)
        knit-drone.pick-up-stitches(cold-person#shoulder-SIDE#location)
        WHILE knit-drone#needle-band#location != cold-person#wrist-SIDE#location
            knit-drone.knit-around(cold-person#wrist-SIDE#location)
        knit-drone.bind-off
        knit-drone.cut-yarn()
        knit-drone.disassemble-needle-band()
    vehicle.pack-up(knit-drone)
    cold-person := warm-person

// prepare for things that could go wrong

EXCEPT
    IF
        yarn.run-out()
    THEN
        vehicle.pack-up(knit-drone)
        vehicle.sleep()
    ELSE IF
        NOT cold-person.stand-still-with-arms-out()
    THEN
        knit-drone.cut-yarn()
        knit-drone.disassemble-needle-band()
        vehicle.pack-up(knit-drone)
        vehicle.wander()
        vehicle.find-cold-person(visual-input)

END
```