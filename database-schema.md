# Tables

User(UserID, FirstName, LastName, DateOfBirth, Gender, Handle, LocationID)
 - Primary Key `UserID`
 - Foreign Key `LocationID` references Location
 
The `User` table contains basic information about each user.

`UserID` - The random UUID that uniquely identifies each user.

`FirstName` - The user's first name.

`LastName` - The user's last name.

`DateOfBirth` - The user's date of birth.

`Gender` - The user's gender.

`Handle` - The user's username

`LocationID` - The random UUID that uniquely identifies a relation in the Location table

---

Event(EventID, HostUserID, LocationID, MinAge, MaxAge, Occupancy, FriendsOnly, Type, Time, Hook, Description)
 - Primary Key `EventID`
 - Foreign Key `HostUserID` references User
 - Foreign Key `LocationID` references Location
 
The `Event` table contains information about a specific event.

`EventID` - The random UUID that uniquely identifies each event.

`HostUserID` - The random UUID that uniquely identifies a relation in the User table.

`MinAge` - The minimum age of an attendee for the event.

`MaxAge` - The maximum age of an attendee for the event.

`Occupancy` - The max occupancy of the event.

`FriendsOnly` - The boolean value to determine if event attendee scope is set for friends only or others as well.

`Type` - The type of event that is selected from a predefined list.

`Time` - The start time of the event.

`Hook` - The single line hook for each event that will hook prospective attendees.

`Description` - The description set by the event creator of the event.

---

Location(LocationID, HostID, AddressID, Latitude, Longitude)
 - Primary Key `LocationID`
 - Foreign Key `HostID` references User
 - Foreign key `AddressID` references Address
 
The `Location` table has granular information about a specific location.

`LocationID` - The random UUID that uniquely identifies a relation.

`HostID` - The random UUID of a relation in the User table.

`AddressID` - The random UUID of a relation in the Address table.

`Latitude` - The latitude corresponding to the event.

`Longitude` - The longitude corresponding to the event.

---

Address(AddressID, AddressLine1, AddressLine2, City, State, ZIP)
 - Primary key `AddressID`

The `Address` table has information about a specific address

`AddressID` - The random UUID that uniquely identifies each address

`AddressLine1` - The address line of the event.

`AddressLine2` - The secondary address of the event (apartment number, etc).

`City` - The city in which the event takes place.

`State` - The state in which the event takes place.

`ZIP` - The ZIP code in which the event takes place. 

---

EventFeed(UserID, EventID)
 - Composite Key `UserID` references User
 - Composite Key `EventID` references Event
 
The `EventFeed` describes each event viewable by each user.

`UserID` - The random UUID of a relation in the user table whose feed includes this event

`EventID` - The random UUID of a relation in the event table

# Potential Tables for New Features

EventTags(Name, Description)
 - Primary Key `Name`
 
The `Friend` describes the friend relationships between users. The `Friend1` attribute is always lower value of the two friends when their IDs are sorted.

---

Friend(Friend1, Friend2)
 - Composite Key `Friend1` references User
 - Composite Key `Friend2` references User
 
The `Friend` describes the friend relationships between users. The `Friend1` attribute is always lower value of the two friends when their IDs are sorted.

---

Friend(Requester, Receiver)
 - Composite Key `Requester` references User
 - Composite Key `Receiver` references User
 
The `Friend` describes a pending request to become friends.

#### Thoughts

Do we want to store additional information about a friendship? Time as friends, parties attended together, etc.? We can put that info somewhere else and produce it by querying other tables, but it's something to think about. If we want to tie that information specifically to a friendship (thinking about it, probably don’t, but we can talk about it), we might want a new primary key for that.