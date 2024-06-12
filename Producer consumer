#include <iostream>
#include <thread>
#include <mutex>
#include <condition_variable>
#include <queue>
#include <chrono>

std::mutex mtx;
std::condition_variable cv;
std::queue<int> buffer;
const int BUFFER_SIZE = 10;

void producer() {
    for (int i = 0; i < 20; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, []{ return buffer.size() < BUFFER_SIZE; }); // Wait until buffer is not full

        // Produce item and add to buffer
        buffer.push(i);
        std::cout << "Produced: " << i << std::endl;

        lock.unlock();
        cv.notify_all(); // Notify consumer that a new item is available
        std::this_thread::sleep_for(std::chrono::milliseconds(500)); // Simulate production time
    }
}

void consumer() {
    for (int i = 0; i < 20; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, []{ return !buffer.empty(); }); // Wait until buffer is not empty

        // Consume item from buffer
        int item = buffer.front();
        buffer.pop();
        std::cout << "Consumed: " << item << std::endl;

        lock.unlock();
        cv.notify_all(); // Notify producer that a slot is available
        std::this_thread::sleep_for(std::chrono::milliseconds(700)); // Simulate consumption time
    }
}

int main() {
    std::thread producer_thread(producer);
    std::thread consumer_thread(consumer);

    producer_thread.join();
    consumer_thread.join();

    return 0;
}


                                                                       JAVA 



import java.util.ArrayList;

public class Prodcons {
    public static void main(String[] args) {
        ArrayList<Integer> buffer = new ArrayList<Integer>();
        Producer p1 = new Producer(buffer);
        Consumer c1 = new Consumer(buffer);
        
        Thread t1 = new Thread(p1);
        Thread t2 = new Thread(c1);
        t1.start();
        t2.start();
        
    }
}

class Producer implements Runnable {
    private int i = 0;
    int max = 10;
    ArrayList<Integer> buffer;

    public Producer(ArrayList<Integer> buffer) {
        this.buffer = buffer;
    }

    public void run() {
        try {
            while (true) {
                i++;
                produce(i);
            }
        } catch (InterruptedException e) {
            System.out.println("Exception");
        }
    }

    public void produce(int i) throws InterruptedException {
        synchronized (buffer) {
            while (buffer.size() == max) {
                System.out.println("full");
                buffer.wait();
            }
            buffer.add(i);
            synchronized (buffer) {
                buffer.notify();
            }
        }
    }
}
class Consumer implements Runnable {
    private int i = 0;
    int max = 10;
    ArrayList<Integer> buffer;

    public Consumer(ArrayList<Integer> buffer) {
        this.buffer = buffer;
    }

    public void run() {
        try {
            while (true) {
                i--;
                consume(i);
            }
        } catch (InterruptedException e) {
            System.out.println("Exception");
        }
    }

    public void consume(int i) throws InterruptedException {
        synchronized ( buffer) {
            while(buffer.size()==0) {
                System.out.println("Buffer is empty");
                buffer.wait();
            }
            buffer.remove(0);
            synchronized (buffer) {
                buffer.notify();
                
            }
        }
    }
}
