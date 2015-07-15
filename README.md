# DataSharingQuorums
Each node acts as Process and Quorum.
The quorum is statically given to processes at the start, this is no dynamic quorum system, hence needs to be changed for handling failure cases.
Quorums are decided to have minimum overlap and sufficient enough to provide mutual exclusion.
Details:

Main: handles the intializing of Server_Thread and CS_Thread.

Server Thread: initializes the Process Object (1).
CS Thread: Initializes the Application module.

Each of the above threads spawn a new Client Thread whenever required (2).

CS_Check has dual purpose:
1. It acts as middle man between CS_Thread and Process, when requesting Critical Section, CS_Thread goes into wait untill Process gives the permission.
2. It provides the mechanism of Logical clock just for Critical Section, used to verify that there is no overlap between Critical Section execution of multiple processes. This logical clock is different from Process's own logical clock.

PS:
(1) The process object can be converted to a process thread, thereby decoupling it from server mechanism.
(2) Sinle client thread handles all the outgoing requests via  FIFO queue like : Producer-Consumer logic.
