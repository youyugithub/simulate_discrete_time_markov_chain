# simulate_discrete_time_markov_chain
simulate dtmc

```
numSteps = parseObj.Results.numSteps;
X0 = parseObj.Results.X0;

if isempty(X0) % Pick random initial state
    
    X0 = zeros(1,numStates);
    p = randperm(numStates,1);
    X0(p) = 1;
    
end

numSims = sum(X0);
    
X = zeros(1+numSteps,numSims);

for j = 1:numSims
    
    simState = find(X0~=0,1);
    X(1,j) = simState;
    
    X0(simState) = X0(simState)-1;

    for i = 2:(1+numSteps)

        u = rand;
        simState = find(u < cumsum(P(simState,:)),1);
        X(i,j) = simState;

    end

end
```
