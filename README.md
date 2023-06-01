

#include <iostream>
#include <vector>
using namespace std;




int getMinimum(vector<int> &data, vector<bool> &isVisit){
    int mins = INT_MAX;
    int min_Index = 0;
    for(int i=0;i<data.size();i++){
        if(isVisit[i] == false && data[i]<=mins){
            mins = data[i];
            min_Index = i;
        }
    }
    return min_Index;
}


void printOutput(vector<int> &data,int src);


float calculateAvgTime(vector<int> &data,int src){
    int sum = 0;
    for(int time : data){
        sum += time;
    }
    float avg_time  = (float) sum/(data.size()-1);
    cout<<endl;
    cout<<"Average time taken from City "<<src <<" : "<<avg_time<<endl;
    return avg_time;
}


void Dijkstras_algo(vector<vector<int>> &graph, int src){


    int v = graph.size();

    vector<int> data(v,INT_MAX);
    data[src] = 0;

    vector<bool> isVisit(v,false);

    for(int i =0;i<v;i++){
        int u = getMinimum(data,isVisit);
        isVisit[u] = true;


        for(int j=0;j<v;j++){
            int value = graph[u][j] + data[u];
            if(isVisit[j] == false  && graph[u][j] != 0 && data[j]>=value ){
                data[j] = value;
            }
        }

    }
    printOutput(data,src);
    calculateAvgTime(data,src);

}

void printOutput(vector<int> &data,int src){

    for(int i=0;i<data.size();i++){
        cout<<"City "<<src<<" to City "<<i<< " : "<<data[i]<<endl;
    }
}




int main(){

    vector<vector<int>> graph = { { 0,10,0,0,15,5 },
                        { 10,0,10,30,0,0 },
                        { 0,10,0,12,5,0},
                        { 0,30,12,0,0,20},
                        { 15,0,5,0,0,0},
                        { 5,0,0,20,0,0} };


    for(int i=0;i<6;i++){
        Dijkstras_algo(graph,i);
    }

    return 0;
}
