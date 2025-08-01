
# FROM python:3.9

# ADD https://netfree.link/dl/unix-ca.sh /home/netfree-unix-ca.sh 
# RUN cat  /home/netfree-unix-ca.sh | sh
# ENV NODE_EXTRA_CA_CERTS=/etc/ca-bundle.crt
# ENV REQUESTS_CA_BUNDLE=/etc/ca-bundle.crt
# ENV SSL_CERT_FILE=/etc/ca-bundle.crt

# # התקנת כלים בסיסיים + NodeJS 16
# RUN apt-get update && apt-get install -y curl gnupg build-essential

# # הוספת תעודות אבטחה של נטפרי
# # ADD https://netfree.link/dl/unix-ca.sh /home/netfree-unix-ca.sh
# RUN chmod +x /home/netfree-unix-ca.sh && /home/netfree-unix-ca.sh

# # הגדרה ל-pip להשתמש בתעודות הנכונות
# ENV SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt

# # התקנת NodeJS 16 בצורה נכונה
# RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
#     apt-get install -y nodejs && \
#     node -v && npm -v

# # הגדרת תיקיית עבודה
# WORKDIR /app

# # התקנת תלויות פייתון
# COPY requirements.txt .
# RUN pip install --no-cache-dir --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt

# # התקנת תלויות node (אם צריך)
# COPY package*.json ./
# RUN npm install

# # העתקת שאר הקבצים
# COPY . .

# # הרצת build (אם רלוונטי)
# # RUN npm run build   ← אם זה פרויקט React

# # חשיפת פורט
# EXPOSE 5000

# # הרצת Flask
# CMD ["python", "app.py"]

FROM python:3.9

# הוספת תעודות אבטחה של נטפרי
ADD https://netfree.link/dl/unix-ca.sh /home/netfree-unix-ca.sh 
RUN chmod +x /home/netfree-unix-ca.sh && /home/netfree-unix-ca.sh
RUN apt-get update && apt-get install -y ca-certificates
RUN curl -sL https://netfree.link/dl/unix-ca.sh | sh
# התקנת כלים בסיסיים + NodeJS 16
RUN apt-get update && apt-get install -y curl gnupg build-essential && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get install -y nodejs && \
    node -v && npm -v
RUN apt-get update && apt-get install -y ca-certificates
RUN apt-get update && apt-get install -y curl gnupg build-essential ca-certificates
RUN apt-get update && apt-get install -y ca-certificates



# הגדרת תיקיית עבודה
WORKDIR /app

# העתקת קבצים והתקנת תלויות
COPY requirements.txt .
RUN pip install --no-cache-dir --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt


COPY package*.json ./
RUN npm install

# העתקת שאר הקבצים
COPY . .

# הרצת build (אם רלוונטי)
RUN npm run build

# חשיפת פורט
EXPOSE 5000

# הרצת Flask
CMD ["python", "app.py"]
