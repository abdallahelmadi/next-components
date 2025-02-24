python3 -c "print('A' * 10000)" | ./client <PID> <br/>
python3 -c "print('\x00\x07\x1bHello\x1b\x07\x00')" | ./client <PID> <br/>
python3 -c "print('\x00' * 10)" | ./client <PID> <br/>
(for i in {1..1000}; do ./client <PID> "A"; done) <br/>
./client 999999 "Test" <br/>
for i in {1..5}; do ./client <PID> "Message $i" & done <br/>
./client <PID> "" <br/>
python3 -c "print('A' * 10000)" | ./client <PID> & sleep 1 && kill <PID> <br/>
