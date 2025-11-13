# Use official Node-RED image
FROM nodered/node-red:latest

# Copy your flow file into the container
COPY flows.json /data/flows.json

# Expose the Node-RED web UI port
EXPOSE 1880

# Start Node-RED
CMD ["npm", "start", "--", "--userDir", "/data"]
