
FROM python:3.9.19-slim
RUN pip install streamlit
WORKDIR /var
COPY dev.py .
EXPOSE 8501
CMD ["streamlit","run","dev.py"]