# Test
const axios = require('axios');

// Replace these values with your Okta settings
const OKTA_DOMAIN = 'https://{yourOktaDomain}.okta.com'; // e.g., https://dev-123456.okta.com
const CLIENT_ID = '{yourClientId}';
const CLIENT_SECRET = '{yourClientSecret}';
const TOKEN_ENDPOINT = `${OKTA_DOMAIN}/oauth2/default/v1/token`;

async function getAccessToken() {
    try {
        const response = await axios.post(
            TOKEN_ENDPOINT,
            new URLSearchParams({
                grant_type: 'client_credentials',
                scope: 'your.api.scope', // Replace with required API scope
            }),
            {
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded',
                    Authorization: `Basic ${Buffer.from(`${CLIENT_ID}:${CLIENT_SECRET}`).toString('base64')}`,
                },
            }
        );

        console.log('Access Token:', response.data.access_token);
        return response.data.access_token;
    } catch (error) {
        console.error('Error fetching token:', error.response?.data || error.message);
    }
}
