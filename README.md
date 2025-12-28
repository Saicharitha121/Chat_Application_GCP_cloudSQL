#  Real-Time Chat Application Backend (Firestore)

This project demonstrates a **real-time chat backend** built using
**Google Cloud Firestore (Native Mode)**.
It focuses on **data modeling, querying, and security rules**---core
skills required for modern backend and cloud-native applications.

------------------------------------------------------------------------

## Features

-   Firestore (Native mode) enabled
-   `chats` collection for storing chat messages
-   Secure access using Firestore Security Rules
-   Query messages between two users
-   Messages sorted by timestamp
-   Authentication-based access control

------------------------------------------------------------------------

##  Firestore Data Model

### Collection: `chats`

Each document contains:

  Field       Type        Description
  ----------- ----------- ---------------------------------
  sender      string      UID or email of sender
  receiver    string      UID or email of receiver
  message     string      Chat message text
  timestamp   timestamp   Message sent time (server time)

------------------------------------------------------------------------

##  Setup Instructions

### 1️.  Enable Firestore (Native Mode)

-   Go to **GCP Console → Firestore**
-   Select **Native Mode**
-   Choose a region

------------------------------------------------------------------------

### 2️. Insert Sample Chat Messages (Python)

``` python
from google.cloud import firestore
from datetime import datetime

db = firestore.Client()

chats_ref = db.collection("chats")

messages = [
    {"sender": "sai", "receiver": "charitha", "message": "Hi!", "timestamp": datetime.utcnow()},
    {"sender": "charitha", "receiver": "sai", "message": "Hello!", "timestamp": datetime.utcnow()},
]

for msg in messages:
    chats_ref.add(msg)
```

*Insert at least 10 messages using similar structure.*

------------------------------------------------------------------------

### 3️. Query Messages Between Two Users

``` python
query = (
    db.collection("chats")
    .where("sender", "in", ["sai", "charitha"])
    .where("receiver", "in", ["sai", "charitha"])
    .order_by("timestamp")
)

for doc in query.stream():
    print(doc.to_dict())
```

------------------------------------------------------------------------

##  Firestore Security Rules

``` js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /chats/{chatId} {
      allow read, write: if request.auth != null &&
        (request.auth.token.email == resource.data.sender ||
         request.auth.token.email == resource.data.receiver);
    }
  }
}
```


-   Only authenticated users can access Firestore
-   Users can read/write **only chats they are part of**
-   Prevents unauthorized data access

------------------------------------------------------------------------



