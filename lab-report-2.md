# Lab Report 1

## Part 1

### `StringServer`
![Image](lab-report-2-images/StringServerCode1.png)
![Image](lab-report-2-images/StringServerCode2.png)

### `/add-message`
1. ![Image](lab-report-2-images/Server1.png)
From my code, `handleRequest` in `Handler` class and `main` in `StringServer` class are called. `args` in main has the argument [“2020”] which is the port number; `url.getPath()` was `/add-message`; `url.getQuery()` was `?s=Ylesia`. After this call, `currentCount` was updated to 1 and `output` was updated to “1. Ylesia\n”.


2. ![Image](lab-report-2-images/Server2.png)
