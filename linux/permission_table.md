# permission table

![permission bit](img/permission_bit.png)


digit | meaning
------|--------
1 | That file can be executed
2 | That file can be written to
3 | That file can be executed and written to
4 | That file can be read
5 | That file can be read and executed
6 | That file can be written to and read
7 | That file can be read, written to, and executed


*u for user, g for group, o for other users not in the group, a for all users. The default is a*

*+ to add permissions, - to remove permissions, = to set absolute permissions, ignoring existing ones*