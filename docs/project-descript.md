# Outcheck

A project to help easily capture conference session experience as attendees leave the room.

## Project Description

A physical device near the room exit that has simple buttons to indicate the attendees' experience of the talk.
Options, preferably iconic graphics, would be thumbs up, thumbs down, too technical, not technical enough. 

## How It Works

### Glossary

* **Device Key**:  a unique ID generated per conference (or as needed) that is mapped to a particular session room
*  **Timestamp**: the time at which the device sent the user interaction
*  **Intent**: the user chosen opinion of the attended talk
*  Session: a talk presented by a speaker, this is what the **Intents** are about
*  Room: a room that the talk is given in and has a device. Associated to a **Device Key** for mapping


### Room Device

#### Device Activation

Each device would be assigned a **Device Key** and be connected to wifi.
The ****Device Key**** is a generated UUID that is reset by pushing a button on the underside of the unit.
When the new UUID is generated, it is assigned as the **Device Key** for the device, the device submits the **Device Key** to a well known HTTP PUT URL registering the device for data submission.
Ideally, the device would also display the UUID/**Device Key** on the underside of the device.

#### Attendee Submission
Each room device would have 4 buttons which would capture the attendee reaction. 
Upon attendee selection the device would make an HTTP PUT request to a well known url including the time of the operation (**Timestamp**), the **Device Key** of the device, and the button selected,perhaps as simple as a # from 0-3 (**Intent**).
Time resolution is important and should include as much significance as possible.

### Server Software

#### Device Registration

An HTTP application which takes an HTTP PUT of a **Device Key**.
The **Device Key** is stored for future use.

#### Attendee Submission

An http application which takes an HTTP PUT of a **Device Key**, **Timestamp**, and **Intent**.
The data is stored for future use.

#### Admin Application

Administrative Features:

* User login and administration
* Import **Session** schedule and **Rooms** from sched.com
* Associate a **Device Key** with a **Room**, also allow modification to new **Device Key** preserving former data for the **Room**

Analytics:

* Display **Sessions** with **Intents** based on **Room** and **Timestamp** 
