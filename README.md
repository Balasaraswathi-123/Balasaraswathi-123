{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "c4d8ea57",
   "metadata": {},
   "source": [
    "## Cardiovascular risk prediction using machine learning algorithms"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "878f2ba9",
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
  "import seaborn as sns\n",
    "import numpy as np\n",
    "%matplotlib inline"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f085db64",
   "metadata": {},
   "source": [
    "#### Loading the data "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "4d9ee6d3",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Age</th>\n",
       "      <th>Sex</th>\n",
       "      <th>ChestPainType</th>\n",
       "      <th>RestingBP</th>\n",
       "      <th>Cholesterol</th>\n",
       "      <th>FastingBS</th>\n",
       "      <th>RestingECG</th>\n",
       "      <th>MaxHR</th>\n",
       "      <th>ExerciseAngina</th>\n",
       "      <th>Oldpeak</th>\n",
       "      <th>ST_Slope</th>\n",
       "      <th>HeartDisease</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>40</td>\n",
       "      <td>M</td>\n",
       "      <td>ATA</td>\n",
       "      <td>140</td>\n",
       "      <td>289</td>\n",
       "      <td>0</td>\n",
       "      <td>Normal</td>\n",
       "      <td>172</td>\n",
       "      <td>N</td>\n",
       "      <td>0.0</td>\n",
       "      <td>Up</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>49</td>\n",
       "      <td>F</td>\n",
       "      <td>NAP</td>\n",
       "      <td>160</td>\n",
       "      <td>180</td>\n",
       "      <td>0</td>\n",
       "      <td>Normal</td>\n",
       "      <td>156</td>\n",
       "      <td>N</td>\n",
       "      <td>1.0</td>\n",
       "      <td>Flat</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>37</td>\n",
       "      <td>M</td>\n",
       "      <td>ATA</td>\n",
       "      <td>130</td>\n",
       "      <td>283</td>\n",
       "      <td>0</td>\n",
       "      <td>ST</td>\n",
       "      <td>98</td>\n",
       "      <td>N</td>\n",
       "      <td>0.0</td>\n",
       "      <td>Up</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>48</td>\n",
       "      <td>F</td>\n",
       "      <td>ASY</td>\n",
       "      <td>138</td>\n",
       "      <td>214</td>\n",
       "      <td>0</td>\n",
       "      <td>Normal</td>\n",
       "      <td>108</td>\n",
       "      <td>Y</td>\n",
       "      <td>1.5</td>\n",
       "      <td>Flat</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>54</td>\n",
       "      <td>M</td>\n",
       "      <td>NAP</td>\n",
       "      <td>150</td>\n",
       "      <td>195</td>\n",
       "      <td>0</td>\n",
       "      <td>Normal</td>\n",
       "      <td>122</td>\n",
       "      <td>N</td>\n",
       "      <td>0.0</td>\n",
       "      <td>Up</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Age Sex ChestPainType  RestingBP  Cholesterol  FastingBS RestingECG  MaxHR  \\\n",
       "0   40   M           ATA        140          289          0     Normal    172   \n",
       "1   49   F           NAP        160          180          0     Normal    156   \n",
       "2   37   M           ATA        130          283          0         ST     98   \n",
       "3   48   F           ASY        138          214          0     Normal    108   \n",
       "4   54   M           NAP        150          195          0     Normal    122   \n",
       "\n",
       "  ExerciseAngina  Oldpeak ST_Slope  HeartDisease  \n",
       "0              N      0.0       Up             0  \n",
       "1              N      1.0     Flat             1  \n",
       "2              N      0.0       Up             0  \n",
       "3              Y      1.5     Flat             1  \n",
       "4              N      0.0       Up             0  "
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "\n",
    "data=pd.read_csv('heart_1.csv')\n",
    "data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "de112a94",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 918 entries, 0 to 917\n",
      "Data columns (total 12 columns):\n",
      " #   Column          Non-Null Count  Dtype  \n",
      "---  ------          --------------  -----  \n",
      " 0   Age             918 non-null    int64  \n",
      " 1   Sex             918 non-null    object \n",
      " 2   ChestPainType   918 non-null    object \n",
      " 3   RestingBP       918 non-null    int64  \n",
      " 4   Cholesterol     918 non-null    int64  \n",
      " 5   FastingBS       918 non-null    int64  \n",
      " 6   RestingECG      918 non-null    object \n",
      " 7   MaxHR           918 non-null    int64  \n",
      " 8   ExerciseAngina  918 non-null    object \n",
      " 9   Oldpeak         918 non-null    float64\n",
      " 10  ST_Slope        918 non-null    object \n",
      " 11  HeartDisease    918 non-null    int64  \n",
      "dtypes: float64(1), int64(6), object(5)\n",
      "memory usage: 86.2+ KB\n"
     ]
    }
   ],
   "source": [
    "data.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "1c5b8a7e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Age</th>\n",
       "      <th>RestingBP</th>\n",
       "      <th>Cholesterol</th>\n",
       "      <th>FastingBS</th>\n",
       "      <th>MaxHR</th>\n",
       "      <th>Oldpeak</th>\n",
       "      <th>HeartDisease</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>918.000000</td>\n",
       "      <td>918.000000</td>\n",
       "      <td>918.000000</td>\n",
       "      <td>918.000000</td>\n",
       "      <td>918.000000</td>\n",
       "      <td>918.000000</td>\n",
       "      <td>918.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>53.510893</td>\n",
       "      <td>132.396514</td>\n",
       "      <td>198.799564</td>\n",
       "      <td>0.233115</td>\n",
       "      <td>136.809368</td>\n",
       "      <td>0.887364</td>\n",
       "      <td>0.553377</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>9.432617</td>\n",
       "      <td>18.514154</td>\n",
       "      <td>109.384145</td>\n",
       "      <td>0.423046</td>\n",
       "      <td>25.460334</td>\n",
       "      <td>1.066570</td>\n",
       "      <td>0.497414</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>28.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>60.000000</td>\n",
       "      <td>-2.600000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>47.000000</td>\n",
       "      <td>120.000000</td>\n",
       "      <td>173.250000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>120.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>0.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>54.000000</td>\n",
       "      <td>130.000000</td>\n",
       "      <td>223.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>138.000000</td>\n",
       "      <td>0.600000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>60.000000</td>\n",
       "      <td>140.000000</td>\n",
       "      <td>267.000000</td>\n",
       "      <td>0.000000</td>\n",
       "      <td>156.000000</td>\n",
       "      <td>1.500000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>77.000000</td>\n",
       "      <td>200.000000</td>\n",
       "      <td>603.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>202.000000</td>\n",
       "      <td>6.200000</td>\n",
       "      <td>1.000000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              Age   RestingBP  Cholesterol   FastingBS       MaxHR  \\\n",
       "count  918.000000  918.000000   918.000000  918.000000  918.000000   \n",
       "mean    53.510893  132.396514   198.799564    0.233115  136.809368   \n",
       "std      9.432617   18.514154   109.384145    0.423046   25.460334   \n",
       "min     28.000000    0.000000     0.000000    0.000000   60.000000   \n",
       "25%     47.000000  120.000000   173.250000    0.000000  120.000000   \n",
       "50%     54.000000  130.000000   223.000000    0.000000  138.000000   \n",
       "75%     60.000000  140.000000   267.000000    0.000000  156.000000   \n",
       "max     77.000000  200.000000   603.000000    1.000000  202.000000   \n",
       "\n",
       "          Oldpeak  HeartDisease  \n",
       "count  918.000000    918.000000  \n",
       "mean     0.887364      0.553377  \n",
       "std      1.066570      0.497414  \n",
       "min     -2.600000      0.000000  \n",
       "25%      0.000000      0.000000  \n",
       "50%      0.600000      1.000000  \n",
       "75%      1.500000      1.000000  \n",
       "max      6.200000      1.000000  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.describe()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "086f94ee",
   "metadata": {},
   "source": [
    "####  Exploratory Data Analysis:\n",
    " The main goal of EDA is to  get an understanding for which variables are important, visualize the data, and view summary statistics\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "9ea9daa6",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[Text(0, 0, 'Normal'), Text(1, 0, 'Heart Disease')]"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 720x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize=(10,4))\n",
    "g=sns.countplot(x='HeartDisease',data=data)\n",
    "g.set_xticklabels(['Normal','Heart Disease'])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "83387a8c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:>"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 1008x432 with 2 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize=(14,6))\n",
    "sns.heatmap(data.corr(),annot=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "80c82cd7",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "MaxHR          -0.400421\n",
       "Cholesterol    -0.232741\n",
       "RestingBP       0.107589\n",
       "FastingBS       0.267291\n",
       "Age             0.282039\n",
       "Oldpeak         0.403951\n",
       "HeartDisease    1.000000\n",
       "Name: HeartDisease, dtype: float64"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.corr()['HeartDisease'].sort_values()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "f87aee40",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:>"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "data.corr()['HeartDisease'].sort_values().drop('HeartDisease').plot(kind='bar')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "2e64ba58",
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "11def2b4",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Age', ylabel='count'>"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAs0AAAEGCAYAAACeiKhrAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuNCwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8QVMy6AAAACXBIWXMAAAsTAAALEwEAmpwYAAAiE0lEQVR4nO3de7xdZXng8d8DCQYhCoGEBg4x2Fo0QkxCQrlIykXAMhWjiB9SBTpBU6fgBGtxUAcaRT6DBrUF21JaacApODNNEQodJDhGqFJpAuEaIbZECI3clJuUCsk7f+xFODlnrfWuk5x9OSe/7+dzPmfvtddz3mevPHn3c9ZZ+92RUkKSJElStR26nYAkSZLU62yaJUmSpAybZkmSJCnDplmSJEnKsGmWJEmSMsZ0O4Em9txzzzR16tRupyFJkqRRbtWqVU+llCYO3D4imuapU6eycuXKbqchSZKkUS4iflK23cszJEmSpAybZkmSJCnDplmSJEnKGBHXNEuSJCnv5ZdfZv369bz00kvdTqXnjRs3jr6+PsaOHdtof5tmSZKkUWL9+vWMHz+eqVOnEhHdTqdnpZR4+umnWb9+Pfvtt1+jGC/PkCRJGiVeeukl9thjDxvmjIhgjz32GNIZeZtmSZKkUcSGuZmhHiebZkmSJCnDplmSJGkU23XXXbe4v3TpUs4666xh+dnr1q3j6quv3nx/xYoVvPGNb2TmzJnsv//+zJ07lxtuuGHz45dddhlXXXXVsIzdab4RUJK0hYPOKX9BW7XktA5n0n6PfP7A0u1Tzr+3w5lII88rr7yyuWn+nd/5nc3bjzjiiM2N8urVq5k3bx4777wzxxxzDB/72Me6le4280yzJEnSdurJJ5/kpJNOYs6cOcyZM4fvf//7ANxxxx0cdthhzJw5k8MOO4wHH3wQaJ2lPvnkk3nPe97Dcccdx7nnnsttt93GjBkz+OpXvzro58+YMYPzzz+fr33tawAsXryYiy++GIBLLrmEadOmMX36dE455RQAfvGLX7BgwQLmzJnDzJkzue6664DWGe0jjjiCWbNmMWvWLH7wgx8AsGHDBubOncuMGTM44IADuO222wC4+eabOfTQQ5k1axYnn3wyL7zwwjYfK880S5IkjWL//u//zowZMzbf/9nPfsaJJ54IwKJFi/jEJz7BO9/5Th555BGOP/541qxZw1vf+lZuvfVWxowZwy233MJnPvMZli1bBsDtt9/OPffcw4QJE1ixYgUXX3zx5jPLK1asGDT+rFmzWLJkyaDtF110EQ8//DCve93reOaZZwC48MILOfroo7niiit45plnOPjgg3nXu97FpEmTWL58OePGjWPt2rXMnz+flStXcvXVV3P88cfz2c9+lo0bN/Liiy/y1FNP8YUvfIFbbrmFXXbZhS9+8Yt85Stf4fzzz9+m42jTLEmSNIrtvPPOrF69evP9pUuXsnLlSgBuueUWHnjggc2PPffcczz//PM8++yznH766axdu5aI4OWXX968z7HHHsuECRMaj59SKt0+ffp0PvShDzFv3jzmzZsHtM4QX3/99ZvPRr/00ks88sgj7L333px11lmsXr2aHXfckYceegiAOXPmsGDBAl5++WXmzZvHjBkz+N73vscDDzzA4YcfDsAvf/lLDj300Mb5VrFpliRJ2k5t2rSJ22+/nZ133nmL7R//+Mc56qijuPbaa1m3bh1HHnnk5sd22WWXIY1x11138ba3vW3Q9htvvJFbb72V66+/ngsuuID777+flBLLli1j//3332LfxYsXs9dee3H33XezadMmxo0bB8DcuXO59dZbufHGGzn11FM555xz2H333Tn22GO55pprhpRnjtc0S5IkbaeOO+64zdcbA5vPSD/77LPss88+QOvMdJXx48fz/PPPVz5+zz33cMEFF3DmmWdusX3Tpk08+uijHHXUUXzpS1/imWee4YUXXuD444/n0ksv3Xx2+q677tqcz+TJk9lhhx34xje+wcaNGwH4yU9+wqRJk/joRz/KGWecwZ133skhhxzC97//fX784x8D8OKLL24+M70tbJolSZK2U5dccgkrV65k+vTpTJs2jcsuuwyAT33qU3z605/m8MMP39yglpk+fTpjxozhHe94x+Y3At52222bl5w788wzueSSSzjmmGO2iNu4cSMf/vCHOfDAA5k5cyaf+MQn2G233TjvvPN4+eWXmT59OgcccADnnXceAL//+7/PlVdeySGHHMJDDz20+Wz3ihUrmDFjBjNnzmTZsmUsWrSIiRMnsnTpUubPn8/06dM55JBD+NGPfrTNxyqqrjPpJbNnz06vXnsjSWovl5xzyTmNXGvWrCm9FELlyo5XRKxKKc0euK9nmiVJkqQMm2ZJkiQpw6ZZkiRJ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\n",
      "text/plain": [
       "<Figure size 864x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize=(12,4))\n",
    "sns.countplot(x='Age', data=data, hue='HeartDisease')\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "959fb359",
   "metadata": {},
   "source": [
    " We can see that the risk of heart disease is higher from age 50 to 65"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "e06fb391",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Sex', ylabel='count'>"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.countplot(x='Sex', data=data, hue='HeartDisease')\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "505b1871",
   "metadata": {},
   "source": [
    "We can clearly see that risk of heart disease is higher among men than women\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "22c21b0a",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "[Text(0, 0, 'Atypical Angina'),\n",
       " Text(1, 0, 'Non-Anginal Pain'),\n",
       " Text(2, 0, 'Asymptomatic'),\n",
       " Text(3, 0, 'Typical Angina')]"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAmQAAAEGCAYAAADLxYlwAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuNCwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8QVMy6AAAACXBIWXMAAAsTAAALEwEAmpwYAAAmIklEQVR4nO3de7gdVZnv+++PgAQFlUtgAwmGVrwAxgQTmouwQUBsbCFeaIOi0NCiu0GR9rJBtzSKOQcFpRvxcrDFAC3QnKYRRGULtBEENAYJlwQQWhACbG7KTQUhvPuPqoRJspKsJMxVK8n38zzzmVWjRlW9a85atd41alSNVBWSJEnqzhpdByBJkrS6MyGTJEnqmAmZJElSx0zIJEmSOmZCJkmS1LE1uw5gRWy00UY1duzYrsOQJElaqmuvvfahqho10LKVOiEbO3YsM2fO7DoMSZKkpUry28Ut85KlJElSx/qekCUZkeS6JBe38xskuTTJbe37+j11j0lye5Jbk+zd79gkSZKGg6FoITsSuLln/mjg8qraCri8nSfJ1sAUYBvgrcDXk4wYgvgkSZI61dc+ZElGA28DpgL/0BbvB+zWTp8BTAf+Z1t+blU9BdyR5HZge+CafsYoSZIG5+mnn2bu3Lk8+eSTXYcyrI0cOZLRo0ez1lprDXqdfnfq/yfgU8B6PWWbVNV9AFV1X5KN2/LNgZ/31Jvblj1PksOAwwC22GKLPoQsSZIGMnfuXNZbbz3Gjh1Lkq7DGZaqiocffpi5c+ey5ZZbDnq9vl2yTPLXwANVde1gVxmgbJGRz6vqtKqaWFUTR40a8M5RSZLUB08++SQbbrihydgSJGHDDTdc5lbEfraQ7Qzsm2QfYCTw0iT/CtyfZNO2dWxT4IG2/lxgTM/6o4F7+xifJElaRiZjS7c8n1HfWsiq6piqGl1VY2k66/9nVR0IXAQc1FY7CLiwnb4ImJJk7SRbAlsBM/oVnyRJ0nDRxXPITgD2SnIbsFc7T1XNBs4D5gCXAIdX1bwO4pMkSYO07rrrPm9+2rRpHHHEES/Itu+8807OPvvsBfPTp0/nZS97GRMmTOA1r3kNu+66KxdffPGC5d/85jc588wzX5B9D7UheVJ/VU2nuZuSqnoY2GMx9abS3JEpSRpm7vr867sOoa+2OPbGrkNQj2eeeWZBQvbe9753Qfkuu+yyIAmbNWsWkydPZp111mGPPfbgwx/+cFfhrjCf1C9JkvriwQcf5F3veheTJk1i0qRJXHXVVQDMmDGDnXbaiQkTJrDTTjtx6623Ak3r2v7778/b3/523vKWt3D00Udz5ZVXMn78eE4++eRFtj9+/HiOPfZYTj31VACOO+44TjrpJABOOeUUtt56a8aNG8eUKVMA+MMf/sAhhxzCpEmTmDBhAhde2PSauvPOO9lll13Ybrvt2G677bj66qsBuO+++9h1110ZP3482267LVdeeSUAP/7xj9lxxx3Zbrvt2H///XniiSdW+LNaqceylCRJ3frTn/7E+PHjF8z/7ne/Y9999wXgyCOP5KijjuJNb3oTd911F3vvvTc333wzr33ta7niiitYc801ueyyy/j0pz/N+eefD8A111zDDTfcwAYbbMD06dM56aSTFrSITZ8+fZH9b7fddpx44omLlJ9wwgnccccdrL322jzyyCMATJ06lTe/+c2cfvrpPPLII2y//fbsueeebLzxxlx66aWMHDmS2267jQMOOICZM2dy9tlns/fee/OZz3yGefPm8cc//pGHHnqIL3zhC1x22WW85CUv4Ytf/CJf+cpXOPbYY1foczQhkyRJy22dddZh1qxZC+anTZvGzJkzAbjsssuYM2fOgmWPPfYYjz/+OI8++igHHXQQt912G0l4+umnF9TZa6+92GCDDQa9/6pFnpAFwLhx43jf+97H5MmTmTx5MtC0bF100UULWtGefPJJ7rrrLjbbbDOOOOIIZs2axYgRI/j1r38NwKRJkzjkkEN4+umnmTx5MuPHj+enP/0pc+bMYeeddwbgz3/+MzvuuOOg410cEzJJktQXzz77LNdccw3rrLPO88o/8pGPsPvuu3PBBRdw5513sttuuy1Y9pKXvGSZ9nHdddfxute9bpHyH/zgB1xxxRVcdNFFHH/88cyePZuq4vzzz+c1r3nN8+oed9xxbLLJJlx//fU8++yzjBw5EoBdd92VK664gh/84Ae8//3v55Of/CTrr78+e+21F+ecc84yxbk09iGTJEl98Za3vGVB/y5gQUvao48+yuabN4PxTJs2bbHrr7feejz++OOLXX7DDTdw/PHHc/jhhz+v/Nlnn+Xuu+9m991350tf+hKPPPIITzzxBHvvvTdf/epXF7SqXXfddQvi2XTTTVljjTU466yzmDevecjDb3/7WzbeeGM++MEPcuihh/KrX/2KHXbYgauuuorbb78dgD/+8Y8LWtRWhAmZJEnqi1NOOYWZM2cybtw4tt56a775zW8C8KlPfYpjjjmGnXfeeUHyM5Bx48ax5ppr8oY3vGFBp/4rr7xywWMvDj/8cE455RT22OP5D2+YN28eBx54IK9//euZMGECRx11FC9/+cv57Gc/y9NPP824cePYdttt+exnPwvA3//933PGGWewww478Otf/3pBK9306dMZP348EyZM4Pzzz+fII49k1KhRTJs2jQMOOIBx48axww47cMstt6zwZ5XFXXtdGUycOLHmX6eWJPWXj73QzTffPODlQS1qoM8qybVVNXGg+raQSZIkdcyETJIkqWMmZJIkSR0zIZMkSeqYCZkkSVLHTMgkSZI65pP6JUlSZ974yTNf0O1de+IHllrnkksu4cgjj2TevHn83d/9HUcfffQLGsPysIVMkiStNubNm8fhhx/Oj370I+bMmcM555zzvPE2u2JCJkmSVhszZszgVa96FX/xF3/Bi170IqZMmcKFF17YdVgmZJIkafVxzz33MGbMmAXzo0eP5p577ukwooYJmSRJWm0MNGRkkg4ieb6+JWRJRiaZkeT6JLOTfK4tPy7JPUlmta99etY5JsntSW5Nsne/YpMkSaun0aNHc/fddy+Ynzt3LptttlmHETX6eZflU8Cbq+qJJGsBP0vyo3bZyVV1Um/lJFsDU4BtgM2Ay5K8uqoWPwy8JEnSMpg0aRK33XYbd9xxB5tvvjnnnnsuZ599dtdh9S8hq6ZN8Il2dq32tWg74XP2A86tqqeAO5LcDmwPXNOvGCVJUrcG85iKF9Kaa67Jqaeeyt577828efM45JBD2GabbYY0hgHj6ufGk4wArgVeBXytqn6R5K+AI5J8AJgJfLyqfg9sDvy8Z/W5bdnC2zwMOAxgiy226Gf4kiRpFbTPPvuwzz77LL3iEOprp/6qmldV44HRwPZJtgW+AbwSGA/cB3y5rT5Qj7pFWtSq6rSqmlhVE0eNGtWXuCVJkobSkNxlWVWPANOBt1bV/W2i9izwLZrLktC0iI3pWW00cO9QxCdJktSlft5lOSrJy9vpdYA9gVuSbNpT7R3ATe30RcCUJGsn2RLYCpjRr/gkSZKGi372IdsUOKPtR7YGcF5VXZzkrCTjaS5H3gl8CKCqZic5D5gDPAMc7h2WkiRpddDPuyxvACYMUP7+JawzFZjar5gkSZKGI5/UL0mS1LG+PvZCkiRpSe76/Otf0O1tceyNS61zyCGHcPHFF7Pxxhtz0003LbX+ULCFTJIkrVYOPvhgLrnkkq7DeB4TMkmStFrZdddd2WCDDboO43lMyCRJkjpmQiZJktQxEzJJkqSOmZBJkiR1zMdeSJKkzgzmMRUvtAMOOIDp06fz0EMPMXr0aD73uc9x6KGHDnkcvUzIJEnSauWcc87pOoRFeMlSkiSpYyZkkiRJHTMhkyRJg1ZVXYcw7C3PZ2RCJkmSBmXkyJE8/PDDJmVLUFU8/PDDjBw5cpnWs1O/JEkalNGjRzN37lwefPDBrkMZ1kaOHMno0aOXaR0TMkmSNChrrbUWW265ZddhrJK8ZClJktSxviVkSUYmmZHk+iSzk3yuLd8gyaVJbmvf1+9Z55gktye5Ncne/YpNkiRpOOlnC9lTwJur6g3AeOCtSXYAjgYur6qtgMvbeZJsDUwBtgHeCnw9yYg+xidJkjQs9C0hq8YT7exa7auA/YAz2vIzgMnt9H7AuVX1VFXdAdwObN+v+CRJkoaLvvYhSzIiySzgAeDSqvoFsElV3QfQvm/cVt8cuLtn9blt2cLbPCzJzCQzvctDkiStCvqakFXVvKoaD4wGtk+y7RKqZ6BNDLDN06pqYlVNHDVq1AsUqSRJUneG5C7LqnoEmE7TN+z+JJsCtO8PtNXmAmN6VhsN3DsU8UmSJHWpn3dZjkry8nZ6HWBP4BbgIuCgttpBwIXt9EXAlCRrJ9kS2AqY0a/4JEmShot+Phh2U+CM9k7JNYDzquriJNcA5yU5FLgL2B+gqmYnOQ+YAzwDHF5V8/oYnyRJ0rDQt4Ssqm4AJgxQ/jCwx2LWmQpM7VdMkiRJw5FP6pckSeqYCZkkSVLHTMgkSZI6ZkImSZLUMRMySZKkjpmQSZIkdcyETJIkqWMmZJIkSR0zIZMkSeqYCZkkSVLHTMgkSZI6ZkImSZLUMRMySZKkjpmQSZIkdcyETJIkqWMmZJIkSR0zIZMkSeqYCZkkSVLH+paQJRmT5CdJbk4yO8mRbflxSe5JMqt97dOzzjFJbk9ya5K9+xWbJEnScLJmH7f9DPDxqvpVkvWAa5Nc2i47uapO6q2cZGtgCrANsBlwWZJXV9W8PsYoSZLUub61kFXVfVX1q3b6ceBmYPMlrLIfcG5VPVVVdwC3A9v3Kz5JkqThYkj6kCUZC0wAftEWHZHkhiSnJ1m/LdscuLtntbkMkMAlOSzJzCQzH3zwwX6GLUmSNCT6npAlWRc4H/hYVT0GfAN4JTAeuA/48vyqA6xeixRUnVZVE6tq4qhRo/oTtCRJ0hDqa0KWZC2aZOy7VfUfAFV1f1XNq6pngW/x3GXJucCYntVHA/f2Mz5JkqThoJ93WQb4NnBzVX2lp3zTnmrvAG5qpy8CpiRZO8mWwFbAjH7FJ0mSNFz08y7LnYH3AzcmmdWWfRo4IMl4msuRdwIfAqiq2UnOA+bQ3KF5uHdYSpKk1UHfErKq+hkD9wv74RLWmQpM7VdMkiRJw5FP6pckSeqYCZkkSVLHTMgkSZI6ZkImSZLUMRMySZKkjpmQSZIkdWxQCVmSywdTJkmSpGW3xOeQJRkJvBjYqB0EfP5zxV4KbNbn2CRJklYLS3sw7IeAj9EkX9fyXEL2GPC1/oUlSZK0+lhiQlZV/wz8c5KPVNVXhygmSZKk1cqghk6qqq8m2QkY27tOVZ3Zp7gkSZJWG4NKyJKcBbwSmAXMH/C7ABMySZKkFTTYwcUnAltXVfUzGEmSpNXRYJ9DdhPw3/oZiCRJ0upqsC1kGwFzkswAnppfWFX79iUqSZKk1chgE7Lj+hmEJEnS6mywd1n+tN+BSJIkra4GO3TS40kea19PJpmX5LGlrDMmyU+S3JxkdpIj2/INklya5Lb2ff2edY5JcnuSW5PsvWI/miRJ0sphUAlZVa1XVS9tXyOBdwGnLmW1Z4CPV9XrgB2Aw5NsDRwNXF5VWwGXt/O0y6YA2wBvBb6eZMTy/FCSJEkrk8HeZfk8VfU94M1LqXNfVf2qnX4cuBnYHNgPOKOtdgYwuZ3eDzi3qp6qqjuA24Htlyc+SZKklclgHwz7zp7ZNWieSzboZ5IlGQtMAH4BbFJV90GTtCXZuK22OfDzntXmtmULb+sw4DCALbbYYrAhSJIkDVuDvcvy7T3TzwB30rRoLVWSdYHzgY9V1WNJFlt1gLJFkr6qOg04DWDixIk+qFaSJK30BnuX5d8uz8aTrEWTjH23qv6jLb4/yaZt69imwANt+VxgTM/qo4F7l2e/kiRJK5PB3mU5OskFSR5Icn+S85OMXso6Ab4N3FxVX+lZdBFwUDt9EHBhT/mUJGsn2RLYCpixLD+MJEnSymiwnfq/Q5MwbUbTr+v7bdmS7Ay8H3hzklntax/gBGCvJLcBe7XzVNVs4DxgDnAJcHhVzRt405IkSauOwfYhG1VVvQnYtCQfW9IKVfUzBu4XBrDHYtaZCkwdZEySJEmrhMG2kD2U5MAkI9rXgcDD/QxMkiRpdTHYhOwQ4G+A/wPcB7wbWK6O/pIkSXq+wV6yPB44qKp+D83wR8BJNImaJEmSVsBgW8jGzU/GAKrqdzQPepUkSdIKGmxCtsZCg4BvwOBb1yRJkrQEg02qvgxcneTfaZ6e/zd4N6QkSdILYrBP6j8zyUyaAcUDvLOq5vQ1MkmSpNXEoC87tgmYSZgkSdILbLB9yCRJktQnJmSSJEkdMyGTJEnqmAmZJElSx0zIJEmSOmZCJkmS1DETMkmSpI6ZkEmSJHXMhEySJKljfUvIkpye5IEkN/WUHZfkniSz2tc+PcuOSXJ7kluT7N2vuCRJkoabfraQTQPeOkD5yVU1vn39ECDJ1sAUYJt2na8nGdHH2CRJkoaNviVkVXUF8LtBVt8POLeqnqqqO4Dbge37FZskSdJw0kUfsiOS3NBe0ly/LdscuLunzty2TJIkaZW35hDv7xvA8UC1718GDgEyQN0aaANJDgMOA9hiiy2WK4g3fvLM5VpvZXHtiR/oOgRJkrQMhrSFrKrur6p5VfUs8C2euyw5FxjTU3U0cO9itnFaVU2sqomjRo3qb8CSJElDYEgTsiSb9sy+A5h/B+ZFwJQkayfZEtgKmDGUsUmSJHWlb5csk5wD7AZslGQu8I/AbknG01yOvBP4EEBVzU5yHjAHeAY4vKrm9Ss2SZKk4aRvCVlVHTBA8beXUH8qMLVf8UiSJA1XPqlfkiSpYyZkkiRJHTMhkyRJ6pgJmSRJUsdMyCRJkjo21E/ql1Y6juwgSeo3W8gkSZI6ZkImSZLUMRMySZKkjpmQSZIkdcyETJIkqWMmZJIkSR0zIZMkSeqYCZkkSVLHTMgkSZI6ZkImSZLUMRMySZKkjpmQSZIkdaxvCVmS05M8kOSmnrINklya5Lb2ff2eZcckuT3JrUn27ldckiRJw82afdz2NOBU4MyesqOBy6vqhCRHt/P/M8nWwBRgG2Az4LIkr66qeX2MT5JeUG/85JlLr7QSu2C9riOQVl19ayGrqiuA3y1UvB9wRjt9BjC5p/zcqnqqqu4Abge271dskiRJw8lQ9yHbpKruA2jfN27LNwfu7qk3ty1bRJLDksxMMvPBBx/sa7CSJElDYbh06s8AZTVQxao6raomVtXEUaNG9TksSZKk/hvqhOz+JJsCtO8PtOVzgTE99UYD9w5xbJIkSZ0Y6oTsIuCgdvog4MKe8ilJ1k6yJbAVMGOIY5MkSepE3+6yTHIOsBuwUZK5wD8CJwDnJTkUuAvYH6CqZic5D5gDPAMc7h2WkiRpddG3hKyqDljMoj0WU38qMLVf8UiSJA1Xw6VTvyRJ0mrLhEySJKljJmSSJEkdMyGTJEnqmAmZJElSx0zIJEmSOmZCJkmS1DETMkmSpI6ZkEmSJHWsb0/ql7RyuOvzr+86hL7Z4tgbuw5BkgbFFjJJkqSOmZBJkiR1zIRMkiSpYyZkkiRJHTMhkyRJ6pgJmSRJUsdMyCRJkjrWyXPIktwJPA7MA56pqolJNgD+DRgL3An8TVX9vov4JEmShlKXLWS7V9X4qprYzh8NXF5VWwGXt/OSJEmrvOF0yXI/4Ix2+gxgcnehSJIkDZ2uErICfpzk2iSHtWWbVNV9AO37xgOtmOSwJDOTzHzwwQeHKFxJkqT+6Wosy52r6t4kGwOXJrllsCtW1WnAaQATJ06sfgUoSZI0VDppIauqe9v3B4ALgO2B+5NsCtC+P9BFbJIkSUNtyBOyJC9Jst78aeAtwE3ARcBBbbWDgAuHOjZJkqQudHHJchPggiTz9392VV2S5JfAeUkOBe4C9u8gNkmSpCE35AlZVf0GeMMA5Q8Dewx1PJIkSV0bTo+9kCRJWi2ZkEmSJHXMhEySJKljJmSSJEkdMyGTJEnqmAmZJElSx0zIJEmSOtbVWJaSJK3W3vjJM7sOoa+uPfEDXYewUjEhWwXd9fnXdx1CX21x7I1dhyBJ0gvKS5aSJEkds4VMkiS94FblqzX9uFJjC5kkSVLHTMgkSZI6ZkImSZLUMRMySZKkjpmQSZIkdcyETJIkqWMmZJIkSR0bdglZkrcmuTXJ7UmO7joeSZKkfhtWCVmSEcDXgL8CtgYOSLJ1t1FJkiT117BKyIDtgdur6jdV9WfgXGC/jmOSJEnqq1RV1zEskOTdwFur6u/a+fcDf1lVR/TUOQw4rJ19DXDrkAc6/G0EPNR1EFppeLxosDxWtCw8Xhb1iqoaNdCC4TaWZQYoe17GWFWnAacNTTgrpyQzq2pi13Fo5eDxosHyWNGy8HhZNsPtkuVcYEzP/Gjg3o5ikSRJGhLDLSH7JbBVki2TvAiYAlzUcUySJEl9NawuWVbVM0mOAP43MAI4vapmdxzWyshLuloWHi8aLI8VLQuPl2UwrDr1S5IkrY6G2yVLSZKk1Y4JmSRJUsdMyFZQknckqSSv7Skbn2SfFdjmxCSnLOe605MMeJtxklFJnk7yoeWNrd3OZkn+fUW2sTpoj4sv98x/IslxL+D2h8X3ubhjri2/Ncn1Sa5K8pp+xbCqG+g8M4T7HpvkvUOwn8m9I7Mk+XySPfu931VFkg2TzGpf/yfJPT3zLxrkNvZd3iELk9yZZKPFLJvQHr97L8+2e7az3H8bVwYmZCvuAOBnNHeEzjceWO6ErKpmVtVHVzCugewP/Jwm5uVWVfdW1btfmJBWaU8B71zcSeoFsDJ8n++rqjcAZwAndhTDqmCg88xQGQv0PSEDJtMMmQdAVR1bVZcNwX5XCVX1cFWNr6rxwDeBk+fPtyPfDGYbF1XVCX0Ib/7xu6Lnqn79bRwWTMhWQJJ1gZ2BQ2lPlO1/Ip8H3tP+Z/KeJLclGdUuX6MdOH2jJNOSfDPJlUl+neSv2zq7Jbl4/j6SfCfJjUluSPKutvwbSWYmmZ3kc4MM+QDg48DoJJv3/BxPJJnatmT8PMkmbfkr2/lftv+tPtGWj01yUzt9cJL/SHJJ+3N+qWe7yxPjquQZmruMjlp4QZJXJLm8/U4vT7JFWz4tySlJrk7ymzSjVyzOyvR9XgG8qt3XlUl+1b52WpYYVkeLOc9smuSK9hxzU5Jdkhya5OSe9T6Y5CvtZ3tLkn9p6343yZ5pWi1vS7J9W/+4JGcl+c+2/IPtpk4Admn3dVSSkT3npOuS7N6uf3CS7yX5fpI7khyR5B/aOj9PskFPXL9sj8/zk7y4PQ72BU5s9/PK9nfh3e06k9rfieuTzEiy3hB9/CuzddrvYS2AJC9N04q1VprW639qP9Obeo6Bg5Oc2k5vkuSC9jO/vud39XtJrm3PA4ctfveNJAHeDRwMvCXJyLZ8bJKbk3yr3daPk6zTLpuU5tx4TZITe84NvX8bj0tyevuz/CbJR3v2uUwxDhtV5Ws5X8CBwLfb6auB7drpg4FTe+r9I/CxdvotwPnt9DTgEprEeCuaB+OOBHYDLm7rfBH4p55trd++b9C+jwCmA+Pa+enAxAFiHQPc1k7/P8A/9Cwr4O3t9JeA/9VOXwwc0E5/GHiinR4L3NTzs/4GeFkb+2+BMUuKcXV5AU8ALwXubD+fTwDHtcu+DxzUTh8CfK/nmPj/22Nia5qxXQfa9rD5PpdwzC0oBz4J/BvwYmBkW7YVMHNZYlgdXwxwnqFJxD/T832sB7wE+C9grZ66r28/22fa6TWAa4HTaUZG2a/n2DsOuB5Yh2bIm7uBzeg5H7X1Pg58p51+LXBX+z0dDNzexjIKeBT4cFvvZJ47B27Ys60vAB/pOfbf3bNsGs0f8he1x8OktvylwJpdfy/D+dV+l58AvgNMbssOA77cTk8HvtVO77rQ796p7fS/9XxnI4CXtdPzzwPrADfN/z5pznMbDRDLm4DL2+mzgXe20/OPy/Ht/HnAge30TcBO7fQJPfEtOBbbn/FqYO32eH2459gfMMbh/rKFbMUcQDMAOu374ppjTwc+0E4fQvNLMt95VfVsVd1Gc9JZuI/InsDX5s9U1e/byb9J8ivgOmAbepr6F2MKzQE/UKx/pvljDc3Jemw7vSNNcgDNL9LiXF5Vj1bVk8Ac4BXLGeMqp6oeA84EFm5m35HnPtOzaE5a832vPSbmAJssZtMry/f53SSzaFp4PgGsBXwryY1tLIvbxuJiWB0NdJ75JfC3afokvr6qHq+qPwD/Cfx1mr5ma1XVje16d1TVjVX1LDCb5vMt4EaeOz4ALqyqP1XVQ8BPgO0HiOdNNMcsVXULTcL86nbZT9pYHqRJyL7flvfuZ9u2lfRG4H00x9KSvAa4r6p+2e7zsap6ZinrqPEvwN+203/L8//2nANQVVcAL03y8oXWfTPwjbbOvKp6tC3/aJLrabpLjKH5x2pJlvR38o6qmtVOXwuMbeNYr6qubsuXdK76QVU91R6vD/Dc+XJZYxwWhtWDYVcmSTakOWC3TVI0/0FUkk8tXLeq7k5yf5I3A39JcxJasHjh6gvvauGyJFvS/HGbVFW/TzKN5j/UJTkA2CTJ/H1vlmSrNhF8uj05A8xj2Y+Lp3qm5wFrLmeMq6p/An7F80+GC+v9jns/zwAkmQq8DaCaPiIry/f5vqqaueCHaRKI+4E30LTWPDnYGAYd/SpkcecZ4FM0LRtvA85KcmJVnUnzB/jTwC08/3jr/Tyf7Zl/lud/tks7H8HAYw4vy36m0bTaXJ/kYJpWjyVZ5Byowamqq9pLg/8dGFFVN/UuXrj60raXZDeaRoIdq+qPSaazhPNAkhHAu4B9k3yG5rvcsOeS88K/5+uw5ONrYQOdq5YpxuHEFrLl927gzKp6RVWNraoxwB00/z0+TtNs3+tfgH+laRGb11O+f5p+Za8E/gK4daH1fgwcMX8myfo0TfZ/AB5N0z/or5YUaJq7215SVZu3sY4F/l+W3kH45zS/TAyi7sKWKcZVWVX9jqY169Ce4qt57jN9H02H1yVt4zPVdtBdyb/Pl9G0djwLvJ8mwdDiLe48syvwQFV9C/g2zWVMquoXNC0C76VtAVlG+6XpI7YhTaL0SxY9n11B+09lklcDW7DoeWtJ1gPua/s29f5zOtB5E5rkcrMkk9p9rpdktUzQl9OZNMfCwv8QvgcgyZuAR3tawOa7HPgfbZ0RSV5K8/v7+zbReS2ww1L2vSdwfVWNaY/fVwDn09zAMaD2KtDjSeZve1nPVcsa47BhQrb8DgAuWKjsfJoT4U+ArdvOqe9pl10ErMuivxS3Aj8FfkTT32LhFoMvAOu3HS+vB3avqutpLhvNprkcetVyxrq0O14+BvxDkhnApjSXIAZlOWJc1X2Zpp/DfB+lueR0A01icuQybGtl/j6/DhyU5Oc0l7n+sJzbWV0s7rueBsxKch1Nkv3PPcvPA67q6d6wLGYAP6BJ3o+vqnuBG4Bn2o7dR9F8hyPaS47/BhxcVU8tdouL+izwC+BSmmRrvnOBT6a5CeCV8wuruUPwPcBX23PgpawkLR7DxHeB9Vk0Qf99kqtp7sg8dJG1mnPS7u33fC3NpeVLaFqhbgCOpzlOlmRJfyeX5FDgtCTX0LSYDfpctRwxDhsOnTRE0jyn6eSq2qWnbBpNB8Vh+fylJC8G/lRVlWQKTYfw/bqOS8vH73P10N6FdnJVXb6M6x1Hc6PHSX0JTJ1Ic6fqflX1/p6y6cAnersTDCdJ1q2q+XeBHw1sWlXL8k/rSslm3yHQHlD/g+c3z68M3gicmiTAIzQ3JGjl5fe5Cms7Q8+guUS0TMmYVk1JvkrTvWC5n4vZkbclOYYmR/ktzd2fqzxbyCRJkjpmHzJJkqSOmZBJkiR1zIRMkiSpYyZkkoaNJP8tyblJ/ivJnCQ/THJYe+fgim57t7Tj8bXzxyW5J8+NB7nvUtb/4QBPM+9d/rV2W3OS/KmdnpUlj0cqSYB3WUoaJtq7Py8Azqiq+YNojwfe/gLtYjea8UWv7ik7uapOSvI64MokG7cPrV1EVS3xTrWqOhyaQZNpHmcz/oUIWtLqwRYyScPF7jTDPn1zfkE7zt2VwLpJ/j3JLUm+2yZvJHljkp8muTbJ/06yaVv+0bal6oa2xW0szYDqR7WtVrv07riqbqYZ6HijJN9rtzc7yWHz6yS5M8lGaYaiuTnJt9o6P06yzkA/UJKzkuzXM//dJPsmOTjJhUkuSXJrkn/sqXNgkhltnP9fmuFnJK3iTMgkDRfb0jwRfCATaEYa2JpmiLGd0wy981Xg3VX1RpoRBKa29Y8GJlTVOJoRMO6keSL5ye0QVFf2bjzJX9KMt/ggcEi7vYk0gxRvOEA8WwFfq6ptaJ7p9q4B6kDP4M5JXgbsBPywXbY9zbMJx9MMoTaxbal7D7Bz28I2j5Xv+YWSloOXLCWtDGZU1VyAJLOAsTSJ0LbApW2D2Qjgvrb+DcB3k3wP+N4StntUkgNpxlF8TzuKwUeTvKNdPoYm+Xp4ofXuaFvvoEkixw608ar6adu3bGPgncD5VfVMG++lVfVw+zP9B804uM/QPMD3l22ddYAHlhC/pFWECZmk4WI2zWDaA+kdK3EezbkrwOyq2nGA+m+jGYB7X+CzSbZZzHZP7h0qKMluNAMi79gOTjydgcdNXDieAS9Zts6iaeWawvNHR1j4qdxF8zOdUVXHLGF7klZBXrKUNFz8J7B2kg/OL0gyCfjvi6l/KzAqyY5t3bWSbJNkDWBMVf0E+BTwcmBdmlaw9ZYSw8uA37fJ2GuBHVbkB2pNo7ncSlXN7infK8kGbf+zyTQDtl8OvLttUaNd/ooXIAZJw5wJmaRhoZpx3N5Bk6j8V5LZwHHAvYup/2eaFrUvJrkemEXTR2sE8K9JbgSuo2kFewT4PvCOgTr197gEWDPJDcDxwM9fgJ/rfuBm4DsLLfoZTevZLJpLmTOrag7wv4AftzFcCmy6ojFIGv4cy1KS+ijJi4Ebge2q6tG27GBgYlUd0WVskoYPW8gkqU+S7AncAnx1fjImSQOxhUySJKljtpBJkiR1zIRMkiSpYyZkkiRJHTMhkyRJ6pgJmSRJUsf+Ly/BQRjfgB+IAAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<Figure size 720x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize=(10,4))\n",
    "g=sns.countplot(x='ChestPainType', data=data, hue='HeartDisease')\n",
    "g.set_xticklabels(['Atypical Angina','Non-Anginal Pain','Asymptomatic','Typical Angina'])\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "37fc3c8e",
   "metadata": {},
   "source": [
    "### DATA Preprocessing:\n",
    "- The main objective is to remove or fill any missing data, remove unnecessary or repetitive features and convert categorical  features to dummy variables."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "7e7ff3a0",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Age               0\n",
       "Sex               0\n",
       "ChestPainType     0\n",
       "RestingBP         0\n",
       "Cholesterol       0\n",
       "FastingBS         0\n",
       "RestingECG        0\n",
       "MaxHR             0\n",
       "ExerciseAngina    0\n",
       "Oldpeak           0\n",
       "ST_Slope          0\n",
       "HeartDisease      0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.isnull().sum()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "814459f6",
   "metadata": {},
   "source": [
    "There is no missing data in this data set"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c7f24298",
   "metadata": {},
   "source": [
    "#### Categorical Variables and Dummy Variables: \n",
    "- Listing all the columns that are currently non-numeric"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "21d62cf9",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Index(['Sex', 'ChestPainType', 'RestingECG', 'ExerciseAngina', 'ST_Slope'], dtype='object')"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "data.select_dtypes(['object']).columns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "22f0183e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Sex_M</th>\n",
       "      <th>ChestPainType_ATA</th>\n",
       "      <th>ChestPainType_NAP</th>\n",
       "      <th>ChestPainType_TA</th>\n",
       "      <th>RestingECG_Normal</th>\n",
       "      <th>RestingECG_ST</th>\n",
       "      <th>ExerciseAngina_Y</th>\n",
       "      <th>ST_Slope_Flat</th>\n",
       "      <th>ST_Slope_Up</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>913</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>914</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>915</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>916</th>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>917</th>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>918 rows × 9 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "     Sex_M  ChestPainType_ATA  ChestPainType_NAP  ChestPainType_TA  \\\n",
       "0        1                  1                  0                 0   \n",
       "1        0                  0                  1                 0   \n",
       "2        1                  1                  0                 0   \n",
       "3        0                  0                  0                 0   \n",
       "4        1                  0                  1                 0   \n",
       "..     ...                ...                ...               ...   \n",
       "913      1                  0                  0                 1   \n",
       "914      1                  0                  0                 0   \n",
       "915      1                  0                  0                 0   \n",
       "916      0                  1                  0                 0   \n",
       "917      1                  0                  1                 0   \n",
       "\n",
       "     RestingECG_Normal  RestingECG_ST  ExerciseAngina_Y  ST_Slope_Flat  \\\n",
       "0                    1              0                 0              0   \n",
       "1                    1              0                 0              1   \n",
       "2                    0              1                 0              0   \n",
       "3                    1              0                 1              1   \n",
       "4                    1              0                 0              0   \n",
       "..                 ...            ...               ...            ...   \n",
       "913                  1              0                 0              1   \n",
       "914                  1              0                 0              1   \n",
       "915                  1              0                 1              1   \n",
       "916                  0              0                 0              1   \n",
       "917                  1              0                 0              0   \n",
       "\n",
       "     ST_Slope_Up  \n",
       "0              1  \n",
       "1              0  \n",
       "2              1  \n",
       "3              0  \n",
       "4              1  \n",
       "..           ...  \n",
       "913            0  \n",
       "914            0  \n",
       "915            0  \n",
       "916            0  \n",
       "917            1  \n",
       "\n",
       "[918 rows x 9 columns]"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dummies=pd.get_dummies(data[['Sex', 'ChestPainType', 'RestingECG', 'ExerciseAngina', 'ST_Slope']],drop_first=True)\n",
    "dummies"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "1982090a",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Age</th>\n",
       "      <th>RestingBP</th>\n",
       "      <th>Cholesterol</th>\n",
       "      <th>FastingBS</th>\n",
       "      <th>MaxHR</th>\n",
       "      <th>Oldpeak</th>\n",
       "      <th>HeartDisease</th>\n",
       "      <th>Sex_M</th>\n",
       "      <th>ChestPainType_ATA</th>\n",
       "      <th>ChestPainType_NAP</th>\n",
       "      <th>ChestPainType_TA</th>\n",
       "      <th>RestingECG_Normal</th>\n",
       "      <th>RestingECG_ST</th>\n",
       "      <th>ExerciseAngina_Y</th>\n",
       "      <th>ST_Slope_Flat</th>\n",
       "      <th>ST_Slope_Up</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>40</td>\n",
       "      <td>140</td>\n",
       "      <td>289</td>\n",
       "      <td>0</td>\n",
       "      <td>172</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>49</td>\n",
       "      <td>160</td>\n",
       "      <td>180</td>\n",
       "      <td>0</td>\n",
       "      <td>156</td>\n",
       "      <td>1.0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>37</td>\n",
       "      <td>130</td>\n",
       "      <td>283</td>\n",
       "      <td>0</td>\n",
       "      <td>98</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>48</td>\n",
       "      <td>138</td>\n",
       "      <td>214</td>\n",
       "      <td>0</td>\n",
       "      <td>108</td>\n",
       "      <td>1.5</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>54</td>\n",
       "      <td>150</td>\n",
       "      <td>195</td>\n",
       "      <td>0</td>\n",
       "      <td>122</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>913</th>\n",
       "      <td>45</td>\n",
       "      <td>110</td>\n",
       "      <td>264</td>\n",
       "      <td>0</td>\n",
       "      <td>132</td>\n",
       "      <td>1.2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>914</th>\n",
       "      <td>68</td>\n",
       "      <td>144</td>\n",
       "      <td>193</td>\n",
       "      <td>1</td>\n",
       "      <td>141</td>\n",
       "      <td>3.4</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>915</th>\n",
       "      <td>57</td>\n",
       "      <td>130</td>\n",
       "      <td>131</td>\n",
       "      <td>0</td>\n",
       "      <td>115</td>\n",
       "      <td>1.2</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>916</th>\n",
       "      <td>57</td>\n",
       "      <td>130</td>\n",
       "      <td>236</td>\n",
       "      <td>0</td>\n",
       "      <td>174</td>\n",
       "      <td>0.0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>917</th>\n",
       "      <td>38</td>\n",
       "      <td>138</td>\n",
       "      <td>175</td>\n",
       "      <td>0</td>\n",
       "      <td>173</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>918 rows × 16 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "     Age  RestingBP  Cholesterol  FastingBS  MaxHR  Oldpeak  HeartDisease  \\\n",
       "0     40        140          289          0    172      0.0             0   \n",
       "1     49        160          180          0    156      1.0             1   \n",
       "2     37        130          283          0     98      0.0             0   \n",
       "3     48        138          214          0    108      1.5             1   \n",
       "4     54        150          195          0    122      0.0             0   \n",
       "..   ...        ...          ...        ...    ...      ...           ...   \n",
       "913   45        110          264          0    132      1.2             1   \n",
       "914   68        144          193          1    141      3.4             1   \n",
       "915   57        130          131          0    115      1.2             1   \n",
       "916   57        130          236          0    174      0.0             1   \n",
       "917   38        138          175          0    173      0.0             0   \n",
       "\n",
       "     Sex_M  ChestPainType_ATA  ChestPainType_NAP  ChestPainType_TA  \\\n",
       "0        1                  1                  0                 0   \n",
       "1        0                  0                  1                 0   \n",
       "2        1                  1                  0                 0   \n",
       "3        0                  0                  0                 0   \n",
       "4        1                  0                  1                 0   \n",
       "..     ...                ...                ...               ...   \n",
       "913      1                  0                  0                 1   \n",
       "914      1                  0                  0                 0   \n",
       "915      1                  0                  0                 0   \n",
       "916      0                  1                  0                 0   \n",
       "917      1                  0                  1                 0   \n",
       "\n",
       "     RestingECG_Normal  RestingECG_ST  ExerciseAngina_Y  ST_Slope_Flat  \\\n",
       "0                    1              0                 0              0   \n",
       "1                    1              0                 0              1   \n",
       "2                    0              1                 0              0   \n",
       "3                    1              0                 1              1   \n",
       "4                    1              0                 0              0   \n",
       "..                 ...            ...               ...            ...   \n",
       "913                  1              0                 0              1   \n",
       "914                  1              0                 0              1   \n",
       "915                  1              0                 1              1   \n",
       "916                  0              0                 0              1   \n",
       "917                  1              0                 0              0   \n",
       "\n",
       "     ST_Slope_Up  \n",
       "0              1  \n",
       "1              0  \n",
       "2              1  \n",
       "3              0  \n",
       "4              1  \n",
       "..           ...  \n",
       "913            0  \n",
       "914            0  \n",
       "915            0  \n",
       "916            0  \n",
       "917            1  \n",
       "\n",
       "[918 rows x 16 columns]"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_d=data.drop(['Sex', 'ChestPainType', 'RestingECG', 'ExerciseAngina', 'ST_Slope'], axis=1)\n",
    "df=pd.concat([df_d,dummies],axis=1)\n",
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "62bef662",
   "metadata": {},
   "source": [
    "### Train Test Split\n",
    "- Splitting The data into training data(70%) and testing data(30%)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "fe2fe1f7",
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "d5507af4",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.model_selection import train_test_split\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "4b1736dc",
   "metadata": {},
   "outputs": [],
   "source": [
    "X=df.drop(['HeartDisease'], axis=1)\n",
    "y=df['HeartDisease']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "c91c78e2",
   "metadata": {},
   "outputs": [],
   "source": [
    "X_train,X_test,y_train,y_test=train_test_split(X,y,train_size=0.3, random_state=42)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "6a7702cc",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.preprocessing import StandardScaler"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "ebd3dd60",
   "metadata": {},
   "outputs": [],
   "source": [
    "scaler=StandardScaler()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "70674142",
   "metadata": {},
   "outputs": [],
   "source": [
    "X_train=scaler.fit_transform(X_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "6bece7f5",
   "metadata": {},
   "outputs": [],
   "source": [
    "X_test=scaler.transform(X_test)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b884f90b",
   "metadata": {},
   "source": [
    "### 1.1  Decision Tree Classifier"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "db42ae65",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.tree import DecisionTreeClassifier"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "23a0b0b3",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-1 {color: black;background-color: white;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-1\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>DecisionTreeClassifier(max_depth=12)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-1\" type=\"checkbox\" checked><label for=\"sk-estimator-id-1\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">DecisionTreeClassifier</label><div class=\"sk-toggleable__content\"><pre>DecisionTreeClassifier(max_depth=12)</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "DecisionTreeClassifier(max_depth=12)"
      ]
     },
     "execution_count": 27,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "dtree = DecisionTreeClassifier(max_depth=12)\n",
    "dtree.fit(X_train,y_train)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "8728588d",
   "metadata": {},
   "source": [
    "### 1.2 Predictions and Evaluations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "1b7f1f7f",
   "metadata": {},
   "outputs": [],
   "source": [
    "predictions_dtree = dtree.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "7deffd2a",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import confusion_matrix,accuracy_score,roc_curve,classification_report\n",
    "from sklearn.model_selection import cross_val_score,GridSearchCV"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "4fe1735d",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Test Accuracy Score :  80.248833592535 \n",
      "\n",
      "\n",
      "10-Fold CV Score :  77.7627806975633 \n",
      "\n",
      "Confusion Matrix : \n",
      " [[226  50]\n",
      " [ 77 290]] \n",
      "\n",
      "\n",
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.75      0.82      0.78       276\n",
      "           1       0.85      0.79      0.82       367\n",
      "\n",
      "    accuracy                           0.80       643\n",
      "   macro avg       0.80      0.80      0.80       643\n",
      "weighted avg       0.81      0.80      0.80       643\n",
      "\n"
     ]
    }
   ],
   "source": [
    "score=accuracy_score(y_test,predictions_dtree)\n",
    "print(\"Test Accuracy Score : \",score*100,'\\n\\n')\n",
    "\n",
    "dtScore=cross_val_score(dtree,X,y,cv=10).mean()*100\n",
    "print(\"10-Fold CV Score : \",dtScore,'\\n')\n",
    "\n",
    "print(\"Confusion Matrix : \\n\",confusion_matrix(y_test,predictions_dtree),'\\n\\n')\n",
    "dt_cr=classification_report(y_test,predictions_dtree)\n",
    "print(dt_cr)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "431e174d",
   "metadata": {},
   "source": [
    "### 2.1 Random Forest Classifier"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "317de265",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-2 {color: black;background-color: white;}#sk-container-id-2 pre{padding: 0;}#sk-container-id-2 div.sk-toggleable {background-color: white;}#sk-container-id-2 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-2 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-2 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-2 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-2 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-2 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-2 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-2 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-2 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-2 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-2 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-2 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-2 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-2 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-2 div.sk-item {position: relative;z-index: 1;}#sk-container-id-2 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-2 div.sk-item::before, #sk-container-id-2 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-2 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-2 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-2 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-2 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-2 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-2 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-2 div.sk-label-container {text-align: center;}#sk-container-id-2 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-2 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-2\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>RandomForestClassifier()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-2\" type=\"checkbox\" checked><label for=\"sk-estimator-id-2\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">RandomForestClassifier</label><div class=\"sk-toggleable__content\"><pre>RandomForestClassifier()</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "RandomForestClassifier()"
      ]
     },
     "execution_count": 31,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.ensemble import RandomForestClassifier\n",
    "rfc = RandomForestClassifier(n_estimators=100)\n",
    "rfc.fit(X_train, y_train)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d4496ad4",
   "metadata": {},
   "source": [
    "#### 2.2 Predictions and Evaluations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "id": "9dcffc33",
   "metadata": {},
   "outputs": [],
   "source": [
    "rfc_pred = rfc.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "id": "ea313c6b",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Test Accuracy Score :  86.62519440124416 \n",
      "\n",
      "\n",
      "10-Fold CV Score :  84.61896798853321 \n",
      "\n",
      "Confusion Matrix : \n",
      " [[243  33]\n",
      " [ 53 314]] \n",
      "\n",
      "\n",
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.82      0.88      0.85       276\n",
      "           1       0.90      0.86      0.88       367\n",
      "\n",
      "    accuracy                           0.87       643\n",
      "   macro avg       0.86      0.87      0.86       643\n",
      "weighted avg       0.87      0.87      0.87       643\n",
      "\n"
     ]
    }
   ],
   "source": [
    "score=accuracy_score(y_test,rfc_pred)\n",
    "print(\"Test Accuracy Score : \",score*100,'\\n\\n')\n",
    "\n",
    "rfScore=cross_val_score(rfc,X,y,cv=10).mean()*100\n",
    "print(\"10-Fold CV Score : \",rfScore,'\\n')\n",
    "\n",
    "print(\"Confusion Matrix : \\n\",confusion_matrix(y_test,rfc_pred),'\\n\\n')\n",
    "rf_cr=classification_report(y_test,rfc_pred)\n",
    "print(rf_cr)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "e5e626be",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-3 {color: black;background-color: white;}#sk-container-id-3 pre{padding: 0;}#sk-container-id-3 div.sk-toggleable {background-color: white;}#sk-container-id-3 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-3 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-3 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-3 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-3 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-3 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-3 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-3 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-3 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-3 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-3 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-3 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-3 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-3 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-3 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-3 div.sk-item {position: relative;z-index: 1;}#sk-container-id-3 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-3 div.sk-item::before, #sk-container-id-3 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-3 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-3 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-3 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-3 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-3 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-3 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-3 div.sk-label-container {text-align: center;}#sk-container-id-3 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-3 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-3\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>SVC()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-3\" type=\"checkbox\" checked><label for=\"sk-estimator-id-3\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">SVC</label><div class=\"sk-toggleable__content\"><pre>SVC()</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "SVC()"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from sklearn.svm import SVC\n",
    "svc=SVC()\n",
    "svc.fit(X_train,y_train)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "6e19ab32",
   "metadata": {},
   "source": [
    "### 3.2 Predictions and Evaluations"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "id": "7f8fed08",
   "metadata": {},
   "outputs": [],
   "source": [
    "pred_svc=svc.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "id": "59d67500",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Test Accuracy Score :  87.09175738724728 \n",
      "\n",
      "\n",
      "10-Fold CV Score :  70.78475871954133 \n",
      "\n",
      "Confusion Matrix : \n",
      " [[245  31]\n",
      " [ 52 315]] \n",
      "\n",
      "\n",
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.82      0.89      0.86       276\n",
      "           1       0.91      0.86      0.88       367\n",
      "\n",
      "    accuracy                           0.87       643\n",
      "   macro avg       0.87      0.87      0.87       643\n",
      "weighted avg       0.87      0.87      0.87       643\n",
      "\n"
     ]
    }
   ],
   "source": [
    "score=accuracy_score(y_test,pred_svc)\n",
    "print(\"Test Accuracy Score : \",score*100,'\\n\\n')\n",
    "\n",
    "svcScore=cross_val_score(svc,X,y,cv=10).mean()*100\n",
    "print(\"10-Fold CV Score : \",svcScore,'\\n')\n",
    "\n",
    "print(\"Confusion Matrix : \\n\",confusion_matrix(y_test,pred_svc),'\\n\\n')\n",
    "svc_cr=classification_report(y_test,pred_svc)\n",
    "print(svc_cr)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e942fa64",
   "metadata": {},
   "source": [
    "#### Hyperparameter tuning: GridSearchCV\n",
    "GridSearchCV takes a dictionary that describes the parameters that should be tried and a model to train. The grid of parameters is defined as a dictionary, where the keys are the parameters and the values are the settings to be tested"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "id": "1119e63a",
   "metadata": {},
   "outputs": [],
   "source": [
    "param_grid = {'C': [0.1,1, 10, 100, 1000], 'gamma': [1,0.1,0.01,0.001,0.0001], 'kernel': ['rbf']} \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "id": "ed75692f",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Fitting 5 folds for each of 25 candidates, totalling 125 fits\n",
      "[CV 1/5] END ........C=0.1, gamma=1, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 2/5] END ........C=0.1, gamma=1, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 3/5] END ........C=0.1, gamma=1, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 4/5] END ........C=0.1, gamma=1, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 5/5] END ........C=0.1, gamma=1, kernel=rbf;, score=0.527 total time=   0.0s\n",
      "[CV 1/5] END ......C=0.1, gamma=0.1, kernel=rbf;, score=0.836 total time=   0.0s\n",
      "[CV 2/5] END ......C=0.1, gamma=0.1, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 3/5] END ......C=0.1, gamma=0.1, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ......C=0.1, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END ......C=0.1, gamma=0.1, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 1/5] END .....C=0.1, gamma=0.01, kernel=rbf;, score=0.855 total time=   0.0s\n",
      "[CV 2/5] END .....C=0.1, gamma=0.01, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END .....C=0.1, gamma=0.01, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END .....C=0.1, gamma=0.01, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END .....C=0.1, gamma=0.01, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END ....C=0.1, gamma=0.001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 2/5] END ....C=0.1, gamma=0.001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 3/5] END ....C=0.1, gamma=0.001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 4/5] END ....C=0.1, gamma=0.001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 5/5] END ....C=0.1, gamma=0.001, kernel=rbf;, score=0.527 total time=   0.0s\n",
      "[CV 1/5] END ...C=0.1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 2/5] END ...C=0.1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 3/5] END ...C=0.1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 4/5] END ...C=0.1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 5/5] END ...C=0.1, gamma=0.0001, kernel=rbf;, score=0.527 total time=   0.0s\n",
      "[CV 1/5] END ..........C=1, gamma=1, kernel=rbf;, score=0.673 total time=   0.0s\n",
      "[CV 2/5] END ..........C=1, gamma=1, kernel=rbf;, score=0.636 total time=   0.0s\n",
      "[CV 3/5] END ..........C=1, gamma=1, kernel=rbf;, score=0.673 total time=   0.0s\n",
      "[CV 4/5] END ..........C=1, gamma=1, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 5/5] END ..........C=1, gamma=1, kernel=rbf;, score=0.709 total time=   0.0s\n",
      "[CV 1/5] END ........C=1, gamma=0.1, kernel=rbf;, score=0.836 total time=   0.0s\n",
      "[CV 2/5] END ........C=1, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END ........C=1, gamma=0.1, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ........C=1, gamma=0.1, kernel=rbf;, score=0.836 total time=   0.0s\n",
      "[CV 5/5] END ........C=1, gamma=0.1, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 1/5] END .......C=1, gamma=0.01, kernel=rbf;, score=0.836 total time=   0.0s\n",
      "[CV 2/5] END .......C=1, gamma=0.01, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 3/5] END .......C=1, gamma=0.01, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END .......C=1, gamma=0.01, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 5/5] END .......C=1, gamma=0.01, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 1/5] END ......C=1, gamma=0.001, kernel=rbf;, score=0.836 total time=   0.0s\n",
      "[CV 2/5] END ......C=1, gamma=0.001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END ......C=1, gamma=0.001, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ......C=1, gamma=0.001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END ......C=1, gamma=0.001, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 1/5] END .....C=1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 2/5] END .....C=1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 3/5] END .....C=1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 4/5] END .....C=1, gamma=0.0001, kernel=rbf;, score=0.509 total time=   0.0s\n",
      "[CV 5/5] END .....C=1, gamma=0.0001, kernel=rbf;, score=0.527 total time=   0.0s\n",
      "[CV 1/5] END .........C=10, gamma=1, kernel=rbf;, score=0.691 total time=   0.0s\n",
      "[CV 2/5] END .........C=10, gamma=1, kernel=rbf;, score=0.636 total time=   0.0s\n",
      "[CV 3/5] END .........C=10, gamma=1, kernel=rbf;, score=0.727 total time=   0.0s\n",
      "[CV 4/5] END .........C=10, gamma=1, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 5/5] END .........C=10, gamma=1, kernel=rbf;, score=0.709 total time=   0.0s\n",
      "[CV 1/5] END .......C=10, gamma=0.1, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 2/5] END .......C=10, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END .......C=10, gamma=0.1, kernel=rbf;, score=0.891 total time=   0.0s\n",
      "[CV 4/5] END .......C=10, gamma=0.1, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 5/5] END .......C=10, gamma=0.1, kernel=rbf;, score=0.727 total time=   0.0s\n",
      "[CV 1/5] END ......C=10, gamma=0.01, kernel=rbf;, score=0.873 total time=   0.0s\n",
      "[CV 2/5] END ......C=10, gamma=0.01, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END ......C=10, gamma=0.01, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ......C=10, gamma=0.01, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END ......C=10, gamma=0.01, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END .....C=10, gamma=0.001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 2/5] END .....C=10, gamma=0.001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 3/5] END .....C=10, gamma=0.001, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END .....C=10, gamma=0.001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 5/5] END .....C=10, gamma=0.001, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END ....C=10, gamma=0.0001, kernel=rbf;, score=0.836 total time=   0.0s\n",
      "[CV 2/5] END ....C=10, gamma=0.0001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END ....C=10, gamma=0.0001, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ....C=10, gamma=0.0001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END ....C=10, gamma=0.0001, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 1/5] END ........C=100, gamma=1, kernel=rbf;, score=0.691 total time=   0.0s\n",
      "[CV 2/5] END ........C=100, gamma=1, kernel=rbf;, score=0.636 total time=   0.0s\n",
      "[CV 3/5] END ........C=100, gamma=1, kernel=rbf;, score=0.727 total time=   0.0s\n",
      "[CV 4/5] END ........C=100, gamma=1, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 5/5] END ........C=100, gamma=1, kernel=rbf;, score=0.709 total time=   0.0s\n",
      "[CV 1/5] END ......C=100, gamma=0.1, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 2/5] END ......C=100, gamma=0.1, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 3/5] END ......C=100, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 4/5] END ......C=100, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END ......C=100, gamma=0.1, kernel=rbf;, score=0.727 total time=   0.0s\n",
      "[CV 1/5] END .....C=100, gamma=0.01, kernel=rbf;, score=0.855 total time=   0.0s\n",
      "[CV 2/5] END .....C=100, gamma=0.01, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 3/5] END .....C=100, gamma=0.01, kernel=rbf;, score=0.873 total time=   0.0s\n",
      "[CV 4/5] END .....C=100, gamma=0.01, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 5/5] END .....C=100, gamma=0.01, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END ....C=100, gamma=0.001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 2/5] END ....C=100, gamma=0.001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END ....C=100, gamma=0.001, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ....C=100, gamma=0.001, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 5/5] END ....C=100, gamma=0.001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 1/5] END ...C=100, gamma=0.0001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 2/5] END ...C=100, gamma=0.0001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 3/5] END ...C=100, gamma=0.0001, kernel=rbf;, score=0.909 total time=   0.0s\n",
      "[CV 4/5] END ...C=100, gamma=0.0001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END ...C=100, gamma=0.0001, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END .......C=1000, gamma=1, kernel=rbf;, score=0.691 total time=   0.0s\n",
      "[CV 2/5] END .......C=1000, gamma=1, kernel=rbf;, score=0.636 total time=   0.0s\n",
      "[CV 3/5] END .......C=1000, gamma=1, kernel=rbf;, score=0.727 total time=   0.0s\n",
      "[CV 4/5] END .......C=1000, gamma=1, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 5/5] END .......C=1000, gamma=1, kernel=rbf;, score=0.709 total time=   0.0s\n",
      "[CV 1/5] END .....C=1000, gamma=0.1, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 2/5] END .....C=1000, gamma=0.1, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 3/5] END .....C=1000, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 4/5] END .....C=1000, gamma=0.1, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 5/5] END .....C=1000, gamma=0.1, kernel=rbf;, score=0.727 total time=   0.0s\n",
      "[CV 1/5] END ....C=1000, gamma=0.01, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 2/5] END ....C=1000, gamma=0.01, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 3/5] END ....C=1000, gamma=0.01, kernel=rbf;, score=0.855 total time=   0.0s\n",
      "[CV 4/5] END ....C=1000, gamma=0.01, kernel=rbf;, score=0.709 total time=   0.0s\n",
      "[CV 5/5] END ....C=1000, gamma=0.01, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END ...C=1000, gamma=0.001, kernel=rbf;, score=0.891 total time=   0.0s\n",
      "[CV 2/5] END ...C=1000, gamma=0.001, kernel=rbf;, score=0.800 total time=   0.0s\n",
      "[CV 3/5] END ...C=1000, gamma=0.001, kernel=rbf;, score=0.927 total time=   0.0s\n",
      "[CV 4/5] END ...C=1000, gamma=0.001, kernel=rbf;, score=0.764 total time=   0.0s\n",
      "[CV 5/5] END ...C=1000, gamma=0.001, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 1/5] END ..C=1000, gamma=0.0001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 2/5] END ..C=1000, gamma=0.0001, kernel=rbf;, score=0.818 total time=   0.0s\n",
      "[CV 3/5] END ..C=1000, gamma=0.0001, kernel=rbf;, score=0.891 total time=   0.0s\n",
      "[CV 4/5] END ..C=1000, gamma=0.0001, kernel=rbf;, score=0.782 total time=   0.0s\n",
      "[CV 5/5] END ..C=1000, gamma=0.0001, kernel=rbf;, score=0.818 total time=   0.0s\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-4 {color: black;background-color: white;}#sk-container-id-4 pre{padding: 0;}#sk-container-id-4 div.sk-toggleable {background-color: white;}#sk-container-id-4 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-4 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-4 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-4 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-4 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-4 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-4 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-4 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-4 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-4 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-4 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-4 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-4 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-4 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-4 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-4 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-4 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-4 div.sk-item {position: relative;z-index: 1;}#sk-container-id-4 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-4 div.sk-item::before, #sk-container-id-4 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-4 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-4 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-4 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-4 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-4 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-4 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-4 div.sk-label-container {text-align: center;}#sk-container-id-4 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-4 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-4\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>GridSearchCV(estimator=SVC(),\n",
       "             param_grid={&#x27;C&#x27;: [0.1, 1, 10, 100, 1000],\n",
       "                         &#x27;gamma&#x27;: [1, 0.1, 0.01, 0.001, 0.0001],\n",
       "                         &#x27;kernel&#x27;: [&#x27;rbf&#x27;]},\n",
       "             verbose=3)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item sk-dashed-wrapped\"><div class=\"sk-label-container\"><div class=\"sk-label sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-4\" type=\"checkbox\" ><label for=\"sk-estimator-id-4\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">GridSearchCV</label><div class=\"sk-toggleable__content\"><pre>GridSearchCV(estimator=SVC(),\n",
       "             param_grid={&#x27;C&#x27;: [0.1, 1, 10, 100, 1000],\n",
       "                         &#x27;gamma&#x27;: [1, 0.1, 0.01, 0.001, 0.0001],\n",
       "                         &#x27;kernel&#x27;: [&#x27;rbf&#x27;]},\n",
       "             verbose=3)</pre></div></div></div><div class=\"sk-parallel\"><div class=\"sk-parallel-item\"><div class=\"sk-item\"><div class=\"sk-label-container\"><div class=\"sk-label sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-5\" type=\"checkbox\" ><label for=\"sk-estimator-id-5\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">estimator: SVC</label><div class=\"sk-toggleable__content\"><pre>SVC()</pre></div></div></div><div class=\"sk-serial\"><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-6\" type=\"checkbox\" ><label for=\"sk-estimator-id-6\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">SVC</label><div class=\"sk-toggleable__content\"><pre>SVC()</pre></div></div></div></div></div></div></div></div></div></div>"
      ],
      "text/plain": [
       "GridSearchCV(estimator=SVC(),\n",
       "             param_grid={'C': [0.1, 1, 10, 100, 1000],\n",
       "                         'gamma': [1, 0.1, 0.01, 0.001, 0.0001],\n",
       "                         'kernel': ['rbf']},\n",
       "             verbose=3)"
      ]
     },
     "execution_count": 38,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "grid=GridSearchCV(SVC(),param_grid,refit=True,verbose=3)\n",
    "grid.fit(X_train,y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "id": "537c25e9",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'C': 1, 'gamma': 0.1, 'kernel': 'rbf'}"
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "grid.best_params_"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "id": "3a3cde5b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-5 {color: black;background-color: white;}#sk-container-id-5 pre{padding: 0;}#sk-container-id-5 div.sk-toggleable {background-color: white;}#sk-container-id-5 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-5 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-5 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-5 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-5 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-5 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-5 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-5 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-5 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-5 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-5 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-5 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-5 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-5 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-5 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-5 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-5 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-5 div.sk-item {position: relative;z-index: 1;}#sk-container-id-5 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-5 div.sk-item::before, #sk-container-id-5 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-5 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-5 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-5 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-5 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-5 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-5 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-5 div.sk-label-container {text-align: center;}#sk-container-id-5 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-5 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-5\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>SVC(C=1, gamma=0.1)</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-7\" type=\"checkbox\" checked><label for=\"sk-estimator-id-7\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">SVC</label><div class=\"sk-toggleable__content\"><pre>SVC(C=1, gamma=0.1)</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "SVC(C=1, gamma=0.1)"
      ]
     },
     "execution_count": 40,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "grid.best_estimator_"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "ec1ae325",
   "metadata": {},
   "outputs": [],
   "source": [
    "grid_predictions=grid.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "id": "875a7c89",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Test Accuracy Score :  87.09175738724728 \n",
      "\n",
      "\n",
      "10-Fold CV Score :  70.78475871954133 \n",
      "\n",
      "Confusion Matrix : \n",
      " [[248  28]\n",
      " [ 55 312]] \n",
      "\n",
      "\n",
      "              precision    recall  f1-score   support\n",
      "\n",
      "           0       0.82      0.90      0.86       276\n",
      "           1       0.92      0.85      0.88       367\n",
      "\n",
      "    accuracy                           0.87       643\n",
      "   macro avg       0.87      0.87      0.87       643\n",
      "weighted avg       0.88      0.87      0.87       643\n",
      "\n"
     ]
    }
   ],
   "source": [
    "score=accuracy_score(y_test,grid_predictions)\n",
    "print(\"Test Accuracy Score : \",score*100,'\\n\\n')\n",
    "\n",
    "gridScore=cross_val_score(svc,X,y,cv=10).mean()*100\n",
    "print(\"10-Fold CV Score : \",gridScore,'\\n')\n",
    "\n",
    "print(\"Confusion Matrix : \\n\",confusion_matrix(y_test,grid_predictions),'\\n\\n')\n",
    "grid_svc_cr=classification_report(y_test,grid_predictions)\n",
    "print(grid_svc_cr)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "73259501",
   "metadata": {},
   "source": [
    "#### Comparing models based on metric evaluation\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "d8797db7",
   "metadata": {},
   "outputs": [],
   "source": [
    "from sklearn.metrics import accuracy_score\n",
    "from sklearn.metrics import f1_score\n",
    "from sklearn.metrics import precision_score\n",
    "from sklearn.metrics import recall_score"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "id": "0c3d8c2a",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Accuracy Scores\n",
    "dt_acc = accuracy_score(y_test,predictions_dtree)\n",
    "rfc_acc = accuracy_score(y_test,rfc_pred)\n",
    "svc_acc = accuracy_score(y_test,pred_svc)\n",
    "gid_svc_acc = accuracy_score(y_test,grid_predictions)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "id": "5ce3adb0",
   "metadata": {},
   "outputs": [],
   "source": [
    "dt_pre = precision_score(y_test,predictions_dtree)\n",
    "rfc_pre = precision_score(y_test,rfc_pred)\n",
    "svc_pre = precision_score(y_test,pred_svc)\n",
    "grid_svc_pre = precision_score(y_test,grid_predictions)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "id": "5c98db18",
   "metadata": {},
   "outputs": [],
   "source": [
    "dt_rcc = recall_score(y_test,predictions_dtree)\n",
    "rfc_rcc = recall_score(y_test,rfc_pred)\n",
    "svc_rcc = recall_score(y_test,pred_svc)\n",
    "grid_svc_rcc = recall_score(y_test,grid_predictions)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "id": "2a8578b4",
   "metadata": {},
   "outputs": [],
   "source": [
    "dt_f1 = f1_score(y_test,predictions_dtree)\n",
    "rfc_f1 = f1_score(y_test,rfc_pred)\n",
    "svc_f1 = f1_score(y_test,pred_svc)\n",
    "grid_svc_f1 = f1_score(y_test,grid_predictions)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "id": "79ec7e76",
   "metadata": {},
   "outputs": [],
   "source": [
    "Model = ['Decision Trees', 'Random Forest', 'SVC','SVC-gridcv']\n",
    "Accuracy = [dt_acc, rfc_acc, svc_acc, gid_svc_acc]\n",
    "Precision=[dt_pre,rfc_pre,svc_pre,grid_svc_pre]\n",
    "Recall=[dt_rcc,rfc_rcc,svc_rcc,grid_svc_rcc]\n",
    "F1Score=[dt_f1,rfc_f1,svc_f1,grid_svc_f1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "id": "232f679c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Accuracy</th>\n",
       "      <th>Precision</th>\n",
       "      <th>Recall</th>\n",
       "      <th>F1_Score</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Model</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Decision Trees</th>\n",
       "      <td>0.802488</td>\n",
       "      <td>0.852941</td>\n",
       "      <td>0.790191</td>\n",
       "      <td>0.820368</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Random Forest</th>\n",
       "      <td>0.866252</td>\n",
       "      <td>0.904899</td>\n",
       "      <td>0.855586</td>\n",
       "      <td>0.879552</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>SVC</th>\n",
       "      <td>0.870918</td>\n",
       "      <td>0.910405</td>\n",
       "      <td>0.858311</td>\n",
       "      <td>0.883590</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>SVC-gridcv</th>\n",
       "      <td>0.870918</td>\n",
       "      <td>0.917647</td>\n",
       "      <td>0.850136</td>\n",
       "      <td>0.882603</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                Accuracy  Precision    Recall  F1_Score\n",
       "Model                                                  \n",
       "Decision Trees  0.802488   0.852941  0.790191  0.820368\n",
       "Random Forest   0.866252   0.904899  0.855586  0.879552\n",
       "SVC             0.870918   0.910405  0.858311  0.883590\n",
       "SVC-gridcv      0.870918   0.917647  0.850136  0.882603"
      ]
     },
     "execution_count": 49,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "performance = pd.DataFrame({'Model':Model,\n",
    "                                        'Accuracy':Accuracy,\n",
    "                                        'Precision':Precision,\n",
    "                                        'Recall':Recall,\n",
    "                                        'F1_Score':F1Score})\n",
    "performance.set_index('Model')\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f03ab6b4",
   "metadata": {},
   "source": [
    "#### Summary:\n",
    "- Support Vector Classifier, SVC with hyper parameter tuning performed better when compared to Descision Trees and Random Forest Classifier\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "fa42a81b",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.8"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
    
        
        
        
       
