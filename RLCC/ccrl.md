### testing using trained agent

#### server
```
cd pcc-uspace/src 
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/airman/Github/ccrl/src/core/ 
./app/pccserver recv {port number}
```
#### sender
```
cd pcc-uspace/src 
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/airman/Github/ccrl/src/core/

// code 직접 수정시
./app/pccclient send 127.0.0.1 {port number}    

// parameter cmd로 입력시
./app/pccclient send 127.0.0.1 9000 --pcc-rate-control=python -pyhelper=loaded_client -pypath=/home/airman/Github/PCC-RL/src/udt-plugins/testing/ --history-len=10 --pcc-utility-calc=linear --model-path=/home/airman/Github/PCC-RL/src/pcc_saved_models/model_rb/
```


### Online training

### server : 동일하게 열어 줌 
```
cd ccrl/src 
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/airman/Github/ccrl/src/core/ 
./app/pccserver recv {port number}
```
### gym side of the training environment from the pcc-rl repo
```
cd pcc-rl/src/gym/online
python3 shim_solver.py
```

### udt side of the training environment
```
cd ccrl/src 
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/airman/Github/ccrl/src/core/ 
./app/pccclient send 127.0.0.1 9000 --pcc-utility-calc=linear --pcc-rate-control=python -pypath=/home/airman/Github/PCC-RL/src/udt-plugins/training/ -pyhelper=shim --history-len=10
```



### Code 상에서 parameter 수정하는법 - parameter 위치
```
    --pcc-utility-calc=  (line 122)        
    --pcc-rate-control=  (line 137)
                                PCC-Upsace/src/pcc/pcc_sender.pcc
    
    -pypath=    (line 55)            
                    "/home/airman/Github/PCC-RL/src/udt-plugins/testing/"  (with model)
                    "/home/airman/Github/PCC-RL/src/udt-plugins/training/" (online training)
    -pyhelper=  (line 69)
                    "loaded_client"  (with model)
                    "shim"           (online training)
                                PCC-Uspace/src/pcc/rate_control/pcc_python_rc.cpp

    
    --model-path= (line43) 
                    "/home/airman/Github/PCC-RL/src/pcc_saved_models/{model name}/"
    --history-len 
    --input-features
                                PCC-RL/src/udt-plugins/testing/loaded_client.py
    
```