import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib as plt
import sklearn
import pickle
import streamlit as s
from mixed_naive_bayes import MixedNB

pre_drugs=pickle.load(open(r"C:\Users\shubh\Downloads\finalp_drugs.pkl","rb"))
model_drugs=pickle.load(open(r"C:\Users\shubh\Downloads\model_drugs.pkl","rb"))

s.title("Prediction of Drug")
s.subheader("Shubhasri")

age=s.number_input("Type age of a person")
sex=s.radio("Select gender of a person",["F","M"])
bp=s.radio("Select blood pressure of a person",["HIGH","LOW","NORMAL"])
cholesterol=s.radio("Select cholesterol of a person",["HIGH","NORMAL"])
na_to_k=s.number_input("Type na to k level of a person")


f_pre=pre_drugs.transform(pd.DataFrame([[age,sex,bp,cholesterol,na_to_k]],columns=["Age","Sex","BP","Cholesterol","Na_to_K"]))
pred=model_drugs.predict(f_pre)


if pred==0:
  x="DrugY"
elif pred==1:
  x="DrugA"
elif pred==2:
  x="DrugB"
elif pred==3:
  x="DrugC"
else:
  x="DrugX"

if s.button("submit"):
  s.write("The prescribed drug is "+x)
