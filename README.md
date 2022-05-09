TERANSFORMING TEXT:

#1ST PART

def read():
	file = open(r"C:\Users\rahul_000\Desktop\null\input_text.txt")
	text = file.read()
	file.close()
	return text
def transform():
	data = read()
	data = data.split("\n")
	print(data)
	ndata = [] 
	for i in data:
		ndata.append(i.capitalize())
	res = "\n".join(ndata)
	return res
def writer():
	file = open(r"C:\Users\rahul_000\Desktop\null\transformed_text.txt","w")
	res = file.write(transform())
	file.close()
	return res	

#2ND PART

from collections import Counter
def read():
	file = open(r"C:\Users\rahul_000\Desktop\null\input_text.txt")
	text = file.read()
	file.close()
	return text
def transform():
	data = read()
	data = data.lower()
	res = Counter(data.split())
	return str(res)
def writer():
	file = open(r"C:\Users\rahul_000\Desktop\null\transformed_text1.txt","w")
	res = file.write(transform())
	file.close()
	return res
writer()	


 FLASK APP FOR 1ST PART:
 
 
from flask import Flask, render_template, request
from werkzeug.utils import secure_filename
import ETL

app = Flask(__name__)

app.config["UPLOAD_FOLDER"] = "static/"

@app.route('/')
def upload_file():
    return render_template('index.html')


@app.route('/display', methods = ['GET', 'POST'])
def save_file():
    if request.method == 'POST':
        f = request.files['file']
        filename = secure_filename(f.filename)

        f.save(app.config['UPLOAD_FOLDER'] + filename)

        file = open(app.config['UPLOAD_FOLDER'] + filename,"r")
        content = ETL.transform()
        ETL.writer()

        
        
    return render_template('content.html', content=content) 

if __name__ == '__main__':
    app.run(host="0.0.0.0", port=5000, debug = True)

FLASK APP FOR 2ND PART:


from flask import Flask, render_template, request
from werkzeug.utils import secure_filename
import ETLROUND_2

app = Flask(__name__)

app.config["UPLOAD_FOLDER"] = "static/"

@app.route('/')
def upload_file():
    return render_template('index.html')


@app.route('/display', methods = ['GET', 'POST'])
def save_file():
    if request.method == 'POST':
        f = request.files['file']
        filename = secure_filename(f.filename)

        f.save(app.config['UPLOAD_FOLDER'] + filename)

        file = open(app.config['UPLOAD_FOLDER'] + filename,"r")
        content = ETLROUND_2.transform()
        ETLROUND_2.writer()

        
        
    return render_template('content.html', content=content) 

if __name__ == '__main__':
    app.run(host="0.0.0.0", port=5000, debug = True)

