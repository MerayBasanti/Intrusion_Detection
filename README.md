# Network Intrusion Detection System (NIDS) using Deep Learning

This project implements a real-time Network Intrusion Detection System (NIDS) using a Deep Neural Network (DNN) to classify network traffic as either normal or anomalous. The system consists of two main components:

1. **Model Training**: A DNN model trained on network traffic features
2. **Real-time Detection**: A packet sniffer that analyzes live network traffic using the trained model

## Features

- **Deep Learning Model**: A 3-layer DNN achieving 98.63% accuracy on test data
- **Real-time Analysis**: Processes live network traffic and classifies flows
- **Feature Extraction**: Extracts 38 network flow features including:
  - Basic connection features (duration, protocol, bytes transferred)
  - Content features (flag types, error rates)
  - Traffic statistics (same service rate, diff host rate)
- **Attack Detection**: Identifies potential network intrusions/anomalies
- **Logging**: Saves all analyzed flows with predictions to CSV

## Requirements

- Python 3.10
- Required packages:
  - TensorFlow/Keras
  - Scapy (2.5.0)
  - scikit-learn
  - pandas
  - numpy
  - matplotlib
  - seaborn

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/network-intrusion-detection.git
   cd network-intrusion-detection
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### 1. Model Training

The model is pre-trained and saved, but you can retrain it by running:
```bash
python DNN_Model.ipynb
```

### 2. Real-time Detection

Run the packet sniffer (requires admin privileges):
```bash
python Sniffing.ipynb
```

The system will:
- Monitor network traffic
- Group packets into flows (10-second timeout)
- Extract features for each flow
- Classify as normal or attack
- Log results to `features_prediction_log.csv`

## File Structure

- `DNN_Model.ipynb`: Jupyter notebook for model training and evaluation
- `Sniffing.ipynb`: Jupyter notebook for real-time packet analysis
- `dnn_ids_model.h5`: Trained DNN model
- `scaler.pkl`, `le_*.pkl`: Feature transformers
- `Train_data.csv`: Sample training dataset
- `features_prediction_log.csv`: Output log of analyzed flows

## Performance

The trained model achieves:
- **Test Accuracy**: 98.63%
- **Precision/Recall**: 98-99% for both classes

Confusion Matrix:
```
              precision    recall  f1-score   support

           0       0.99      0.98      0.99      2674
           1       0.98      0.99      0.99      2365
```

## Customization

To adapt the system:
1. Update `used_features` in `DNN_Model.ipynb` to select different features
2. Modify `FLOW_TIMEOUT` in `Sniffing.ipynb` to change flow grouping
3. Retrain with your own dataset by replacing `Train_data.csv`

## Limitations

- Currently only analyzes TCP/UDP traffic
- Some statistical features are simplified for real-time processing
- Requires retraining for optimal performance on different networks

## Future Improvements

- Add support for more protocols
- Implement alerting system for detected attacks
- Add GUI dashboard for monitoring
- Incorporate more sophisticated feature extraction

## License

This project is licensed under the MIT License.

---

For questions or contributions, please open an issue or pull request.
