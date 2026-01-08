# CubeScalers

kubectl port-forward --namespace default svc/postgresql-dev 5432:5432 & PGPASSWORD=postgres psql --host 127.0.0.1 -U postgres -d postgres -p 5432



C:\Users\CubeScalers\Desktop\Smart_Autoscaler\data\updated_2_months_data.csv

-- Create Table and copy forecast data to it
CREATE TABLE timeseries_forecast (
  timestamp TIMESTAMP PRIMARY KEY,
  value DECIMAL
);
\copy timeseries_forecast FROM './notebooks/prediction.csv' WITH (FORMAT csv, HEADER true);

\copy timeseries_forecast FROM './Smart_Autoscaler/data/updated_2_months_data.csv' WITH (FORMAT csv, HEADER true);



kubectl apply -f ./Smart_Autoscaler/Kube/keda-scaledobject.yaml

#Verify KEDA is running
kubectl get pods -n keda

#Check KEDA logs
kubectl logs -f keda-operator-7455868854-h79fq -n keda

# 1. Connect to Postgres running in Kubernetes
kubectl port-forward --namespace default svc/postgresql-dev 5432:5432 & PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432

********************************************
taskkill /PID 4601 /F

#psql command for Current time stamp:
SELECT CURRENT_TIMESTAMP;



****************

SELECT MAX(value)
FROM (
  SELECT value
  FROM timeseries_forecast
  WHERE timestamp > CURRENT_TIMESTAMP
  ORDER BY timestamp
  LIMIT 3
) t;


kubectl get pods -n default -l app=greeter
