# INTERACTION BETWEEN USER AND THE SYSTEM

_Interactions between users and the system for key functionalities like user registration, property booking, and payments._

Use case diagram present in this dirextory:
**usecase-diagram.drawio.png**

[User] ------ (Register)
[User] ------ (Login)
[Registered User] ------ (Login)
[Registered User] ------ (Book Property) ----->> (Make Payment) : <<include>>
[Registered User] ------ (Make Payment)
[Registered User] ------ (View Booking History) <<---- (Book Property) : <<extend>>
[Registered User] ------ (Manage Account) <<---- (Login) : <<include>>
