#include <iostream>
#include <limits>
using namespace std;

int main() {
    int blocksize[10], processsize[10], blockno, processno, flags[10], allocation[10], i, j;

    // Initialize flags and allocation arrays
    for(i = 0; i < 10; i++) {
        flags[i] = 0;
        allocation[i] = -1;
    }

    // Entering blocks
    cout<<"Fill the number of blocks: ";
    cin>>blockno;
    cout<<"\nFill size of each block: ";
    for(i = 0; i < blockno; i++)
        cin>>blocksize[i];

    // Entering processes
    cout<<"\nFill the number of processes: ";
    cin>>processno;
    cout<<"\nEnter each process size: ";
    for(i = 0; i < processno; i++)
        cin>>processsize[i];

    // Memory allocation as per best fit
    for(i = 0; i < processno; i++) {
        int bestFitIndex = -1;
        int minFragmentation = numeric_limits<int>::max();
        for(j = 0; j < blockno; j++) {
            if(flags[j] == 0 && blocksize[j] >= processsize[i]) {
                int fragmentation = blocksize[j] - processsize[i];
                if (fragmentation < minFragmentation) {
                    minFragmentation = fragmentation;
                    bestFitIndex = j;
                }
            }
        }
        if (bestFitIndex != -1) {
            allocation[bestFitIndex] = i;
            flags[bestFitIndex] = 1;
        }
    }

    // Display allocation details
    cout<<"\nBlock no.\t size\t \tprocess no. \t \tsize";
    for(i = 0; i < blockno; i++) {
        cout<<"\n"<<i<<"\t\t"<<blocksize[i]<<"\t\t";
        if(flags[i] == 1)
            cout<<allocation[i]<<"\t\t\t"<<processsize[allocation[i]];
        else
            cout<<"Not allocated";
    }

    return 0;
}
