FROM public.ecr.aws/lambda/python:3.11

WORKDIR /app
COPY requirements.txt .
COPY main.py .
# Download and install precompiled SQLite binary
RUN curl -L https://www.sqlite.org/2024/sqlite-tools-linux-x86-3430200.zip -o sqlite.zip && \
    unzip sqlite.zip && \
    mv sqlite-tools-linux-x86-3430200/sqlite3 /usr/local/bin/sqlite3 && \
    chmod +x /usr/local/bin/sqlite3 && \
    rm -rf sqlite.zip sqlite-tools-linux-x86-3430200

RUN pip install --no-cache-dir -r requirements.txt

COPY . .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
