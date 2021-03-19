To approach this project we started understanding TCP protcol from the lecture notes.
When starting to implement the receiver we decided it would be good to hold a dictionary which would contain our
final packets. This dictionary would map a packets SEQUENCE number to the message for later printing to console. This
worked well because if we were to encounter duplicate packets a dictionary only can have one type of a certain key. Thus
whenever we encountered an EOF true flag from the sender we would print out every packet in our dictionary in order
from the lowest packet SEQUENCE number to the highest. We also set an expectedSequence number in this class which would
increment if the sequence was the next from our previously updated sequence number and would override the packet for that
seqeuence number key in our final packets dictionary. For the sender we maintained two dictionaries of buffered packets
and sent packets. Every time a message was sent to the receiver from our sender we would add that message to our buffered
packets. If we got an ACK back for that sequence number we could then pop that packet from our buffered packets and
add it to our sent packets since we have confirmed the recevier got the message. This implentation was good for handling
dropped packets. If we did not get a ACK back for a packet then at the end of our while loop we try and re send any packets
that are still in our buffered packets dictionary. With this implementation for the sender we know that the we are
finished once there are no packets left in our buffered packets and if we try and send a message and the length of the
data is 0 (as was in the starter code). Finally when we know we have sent all the data we try and send an EOF true
flag with no data over to the receiver so that it knows to print all the data. For this we sent the sequence multiple
times in a loop because there could be cases where that last sending EOF true flag could get dropped so sending it
once was sometimes not adequate. (There is prob better implementation for this). To test our code we use the log
function from the starter code and used nettest to debug what our buffered packets and final packets dictionaries
looked like.