python3 -c "print('A' * 10000)" | ./client <PID>
python3 -c "print('\x00\x07\x1bHello\x1b\x07\x00')" | ./client <PID>
python3 -c "print('\x00' * 10)" | ./client <PID>
(for i in {1..1000}; do ./client <PID> "A"; done)
./client 999999 "Test"
for i in {1..5}; do ./client <PID> "Message $i" & done
./client <PID> ""
python3 -c "print('A' * 10000)" | ./client <PID> & sleep 1 && kill <PID>
