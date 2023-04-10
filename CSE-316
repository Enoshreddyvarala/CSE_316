import queue


class Process:
    def __init__(self, process_id, priority, burst_time, arrival_time):
        self.process_id = process_id
        self.priority = priority
        self.burst_time = burst_time
        self.arrival_time = arrival_time


class MultilevelQueueScheduler:
    def __init__(self):
        self.l1 = []  # highest priority queue
        self.l2 = []  # medium priority queue
        self.l3 = []  # lowest priority queue
        self.q1 = queue.Queue()
        self.q2 = queue.Queue()
        self.q3 = queue.Queue()
        self.quantum = 10  # time quantum for each queue
        self.Q1quantum = 2  # time quantum of queue1 round robin
        self.current_time = 0

    def add_process(self, process_id, priority, burst_time, arrival_time):
        proc = Process(process_id, priority, burst_time, arrival_time)
        if priority >= 1 and priority <= 2:
            self.l1.append(proc)
        elif priority >= 3 and priority <= 5:
            self.l2.append(proc)
        else:
            self.l3.append(proc)

    def RUN(self):
        for i in self.l1:
            if i.arrival_time == self.current_time:
                self.q1.put(i)
            if self.q1.empty():
                print("CPU is idel at second :", self.current_time)
                self.current_time += 1
                for i in self.l1:
                    if i.arrival_time == self.current_time:
                        self.q1.put(i)
        for i in self.l2:
            if i.arrival_time == self.current_time:
                if i.priority == 3:
                    self.q2.put(i)
                elif i.priority == 4:
                    self.q2.put(i)
                elif i.priority == 5:
                    self.q2.put(i)
            if self.q2.empty():
                self.current_time +=1
        for i in self.l3:
            if i.arrival_time==self.current_time:
                self.q3.put(i)
            if self.q3.empty():
                self.current_time +=1    
        while not len(self.l1) == 0 or len(self.l2) == 0 or len(self.l3) == 0:
            if not len(self.l1) == 0:
                for x in range(self.quantum):
                    rp=self.q1.get()
                    for n in range(self.Q1quantum):
                        if rp.burst_time > 0:
                            rp.burst_time -= 1
                            self.current_time += 1
                            for i in self.l1:
                                if i.arrival_time == self.current_time:
                                    self.q1.put(i)
                            for i in self.l2:
                                if i.arrival_time == self.current_time:
                                    if i.priority == 3:
                                        self.q2.put(i)
                                    elif i.priority == 4:
                                        self.q2.put(i)
                                    elif i.priority == 5:
                                         self.q2.put(i)
                            for i in self.l3:
                                if i.arrival_time==self.current_time:
                                    self.q3.put(i)
                        else:
                            break
                        if rp.burst_time > 0:
                            self.q1.put(rp)
                        else:
                            print("Process", rp.process_id, "completed at time", self.current_time)

            if not len(self.l2) == 0:  # running queue2 priority schedulling algorithm
                rp1 = self.q2.get()
                for n in range(self.quantum):
                    rp1.burst_time -= 1
                    self.current_time += 1
                    for i in self.l2:
                        if i.arrival_time == self.current_time:
                            if i.priority == 3:
                                self.q2.put(i)
                            elif i.priority == 4:
                                self.q2.put(i)
                            elif i.priority == 5:
                                self.q2.put(i)
                    for i in self.l3:
                        if i.arrival_time==self.current_time:
                            self.q3.put(i)
                    if rp1.burst_time == 0:
                        print("Process", rp1.process_id, "completed at time", self.current_time)
                        rp1 = self.q2.get()
            if not len(self.l3) ==0:
                rp2 = self.q3.get()
                for n in range(self.quantum):
                    rp2.burst_time -=1
                    self.current_time +=1
                    for i in self.l2:
                        if i.arrival_time == self.current_time:
                            if i.priority == 3:
                                self.q2.put(i)
                            elif i.priority == 4:
                                self.q2.put(i)
                            elif i.priority == 5:
                                    self.q2.put(i)
                    for i in self.l3:
                        if i.arrival_time==self.current_time:
                            self.q3.put(i)
                    if rp2.burst_time == 0:
                        print("Process", rp2.process_id, "completed at time", self.current_time)
                        rp2 = self.q3.get()
scheduler = MultilevelQueueScheduler()
num_processes = int(input("Enter number of processes: "))
for i in range(num_processes):
    pid = i + 1
    priority = int(input("Enter priority for process " + str(pid) + ": "))
    burst_time = int(input("Enter burst time for process " + str(pid) + ": "))
    arrival_time = int(input("Enter Arrival time for process " + str(pid) + ":"))
    scheduler.add_process(pid, priority, burst_time, arrival_time)
scheduler.RUN()                    
